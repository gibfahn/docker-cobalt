# Dockerfile for static site generator Cobalt

This repository contains infrastructure for building docker images
containing [Cobalt](https://github.com/cobalt-org/cobalt.rs) binaries.

The docker image is based on `alpine` image. `cobalt` binary in the
image is statically linked with `musl`.

## Overview

Structure:

* `Makefile`
* git submodule `cobalt.rs`
* `Dockerfile` in `dockerfiles`

We use `Makefile` for automating docker image build process. git
submodule `cobalt.rs` contains Cobalt source code. Image version is
taken from submodule using `git descrbie --tags`.

## Build Requirements

* make
* docker client (available without `sudo`)
* cargo
* `x86_64-unknown-linux-musl` rust target

```bash
# Install x86_64-unknown-linux-musl rust target
rustup target add x86_64-unknown-linux-musl

# Install musl-gcc compiler
# Linux:
sudo apt install musl-tools

#macOS
brew install musl-cross
```

## Build Process

Don't forget to checkout `cobalt.rs` submodule:

```bash
git submodule init
git submodule update
```

Build docker images:

```bash
make
```

Publish docker image:

```bash
make push
```

Publish docker image as `latest`:

```bash
make push-latest
```

Long story short, in order to release a new version one needs to:

* update submodule so it points to a correct tag
* build image using `make`
* push image using `make push` (and optionally `make push-latest`)

