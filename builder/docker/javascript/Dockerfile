FROM suborbital/subo:dev as subo
FROM rust:1.56.1-slim-bullseye as rust

WORKDIR /root

RUN apt-get update && \
    apt-get install pkg-config git build-essential libssl-dev clang cmake curl -y && \
    rustup target install wasm32-wasi && \
    cargo install wasmtime-cli cargo-wasi && \
    git clone -b suborbital-v0.2.0 https://github.com/suborbital/javy.git && \
    cd javy && \
    make

FROM node:16-bullseye-slim

RUN mkdir runnable; mkdir suborbital

# Propagate our root permissions for our home folder to everyone. This allows
# npm scripts (which get run as whatever user owns the mounted runnable
# directory) to access common home folder resources (caches, etc.).
RUN chmod -R o=u /root

COPY --from=rust /root/javy/target/release/javy /usr/local/bin
COPY --from=subo /go/bin/subo /usr/local/bin

WORKDIR /root/runnable
