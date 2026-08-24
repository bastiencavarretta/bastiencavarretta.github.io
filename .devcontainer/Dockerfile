FROM mcr.microsoft.com/devcontainers/jekyll

# Fix: Remove the broken Yarn repository from the apt sources.
# This prevents 'apt-get update' from failing due to the missing GPG key.
# (Yarn is already provided by the dev container features/nvm, so this system repo is unnecessary)
# See issue #3487
RUN rm -f /etc/apt/sources.list.d/yarn.list

# Claude Code
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g @anthropic-ai/claude-code \
    && chown -R vscode:vscode /usr/lib/node_modules /usr/bin/claude \
    && rm -rf /var/lib/apt/lists/*
