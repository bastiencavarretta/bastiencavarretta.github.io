# Local hosting for unit-test developpment.

From the container or host, you can build locally your website and display it in your browser by running
`bundle exec jekyll build --watch`
The result will appear in `http://localhost:4000/name_of_website//`
Other parsers `--trace`, `--livereload`

# Converting pdf to png in linux

`pdftoppm -r 150 -png -singlefile <path-to-your-existing-pdf> <desired-path-to-your-png>`

# Macros in Markdown mathjax

    ``$$\newcommand{\RR}{\mathbb{R}}
    \newcommand{\norm}[1]{\left\lVert #1 \right\rVert}$$

    The space $\RR^n$ with norm $\norm{x}$.''

# Before pushing, always run

`npx prettier . --write`
This formats the repo to avoid deployment errors on github.
