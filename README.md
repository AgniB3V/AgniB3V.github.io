# agnib3v.github.io

[AgniB3V.github.io](https://agnib3v.github.io/)

Created using [mdBook](https://rust-lang.github.io/mdBook/)

## Installation

To install using Rust, run:

```
cargo install mdbook
```

Can also be installed using pre-compiled bianries. For more information, see https://rust-lang.github.io/mdBook/guide/installation.html.

## Local execution

To run locally, run:

```
mdbook serve -o docs
```

## Building

To build, just push changes and it will be built using the workflow located in `.github/workflows/deploy.yml`.

It can be built locally using `mdbook build docs`. For more information, see https://rust-lang.github.io/mdBook/cli/build.html.
