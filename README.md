# Cross compilation environment for `rust` targeting [musl](https://www.musl-libc.org/) on ARMHF

Based on the official [Debian stretch](https://github.com/sensorfu/rust-musl-arm.git) image and
[musl-cross-make](https://github.com/richfelker/musl-cross-make) tool to build a
rust cross-compilation development environment.

# Prebuilt images

| Rust toolchain | Cross Compiled Target               |
|----------------|-------------------------------------|
| stable         | arm-unknown-linux-musleabihf        |
| stable         | armv7-unknown-linux-musleabihf      |

# Usage

1. Pull the docker image from docker hub with target tag, e.g. `arm-unknown-linux-musleabihf`

```
$ docker pull skyuplam/rust-musl-armha:<target tag>
```

2. Cross compile target tag, e.g. `arm-unknown-linux-musleabihf` using the docker image

```
$ docker run --rm \
  --volume <path to your rust project>:/home/cross/project \
  --volume <path to your local cargo registry, e.g. ~/.cargo/registry>:/usr/local/cargo/registry \ # optional, advoid cargo to update on every build
  skyuplam/rust-musl-armhf:<target tag> \
  <cargo command> # e.g. `cargo build --release`
```

# Build your own docker image

Change the variables in the `Makefile` and then run:

```
# to build armv7-unknown-linux-musleabihf
$ make TARGET=arm7-unknown-linux-musleabihf build
```

# Supported `TARGET`s

See [`musl-cross-make` repo](https://github.com/richfelker/musl-cross-make#supported-targets)
