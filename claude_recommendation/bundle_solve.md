# Dev container `bundle install` permission failure

## Symptom

`postCreateCommand` fails during container creation:

```
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /usr/local/bundle/gems/bundler-4.0.6 directory.
...
Errno::EACCES: Permission denied @ dir_s_mkdir - /usr/local/bundle/cache/bundler
```

`postCreateCommand from devcontainer.json failed with exit code 1.`

## Root cause

This is a container-permissions bug, not an issue with the al-folio site content.

- `.devcontainer/devcontainer.json` sets `"remoteUser": "vscode"`, so `bundle install` runs as `vscode`.
- `bundle install` is actually invoked by `/usr/local/post-create.sh`, which is baked into the base image `mcr.microsoft.com/devcontainers/jekyll` — our `devcontainer.json` doesn't define its own `postCreateCommand`, so this inherited script is what runs.
- `GEM_HOME` / bundler's install path is `/usr/local/bundle`. By the time `post-create.sh` runs, `vscode` doesn't have write access to it, hence the `Gem::FilePermissionError` / `Errno::EACCES`.
- `.devcontainer/Dockerfile` already tries to fix this:
  ```dockerfile
  RUN chown -R vscode:vscode /usr/local/bundle
  ```
  but that chown runs at **image build time**, inside our Dockerfile stage.
- Dev container **Features** (`ghcr.io/rocker-org/devcontainer-features/apt-packages` installing `ruby-full`, plus `prettier`) are layered **on top of** the Dockerfile as a separate root-run build stage that executes _after_ it. That layer touching Ruby/gems as root is the most likely reason ownership of `/usr/local/bundle` reverts to root before the container actually starts and `post-create.sh` runs — so the chown never survives to the moment `bundle install` needs it.
- A stale cached image built before that chown line existed would produce the identical symptom, so it's worth ruling that out too.

## Fixes

1. **Quick check** — rebuild fully with no cache (`Dev Containers: Rebuild Container Without Cache`) in case the running image just predates the `chown` line.
2. **Robust fix** — stop relying on the build-time chown and re-assert ownership right before `bundle install` runs, by explicitly overriding `postCreateCommand` in `devcontainer.json`:
   ```json
   "postCreateCommand": "sudo chown -R vscode:vscode /usr/local/bundle && sh /usr/local/post-create.sh"
   ```
   This runs after all features are applied, so it can't be undone by them. `vscode` has passwordless sudo in Microsoft's devcontainer base images, so this should just work.

## Status

Not yet applied to `.devcontainer/devcontainer.json` — pending user confirmation.
