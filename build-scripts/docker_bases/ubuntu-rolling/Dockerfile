FROM ubuntu:rolling

LABEL maintainer "alves.rjc+docker@gmail.com"

RUN apt update && \
    apt install -y \
    build-essential \
    cabal-install \
    coreutils \
    curl \
    ghc \
    git \
    libbz2-dev \
    liblzma-dev \
    m4 \
    python-dev \
    python-pip \
    wget \
    xxd \
    xz-utils \
    zlib1g-dev && \
    apt clean && \
    rm -rf /var/lib/apt/lists && \
    wget -qO- https://get.haskellstack.org/ | sh && \
    chmod 755 /usr/local/bin/stack && \
    pip install tox

# Build ngless dependencies to save time during build
RUN git clone https://gitlab.com/ngless/ngless && \
    cd ngless && \
    STACKOPTS="--system-ghc --only-dependencies" make ngless && \
    STACKOPTS="--system-ghc --only-dependencies" make tests && \
    cd .. && \
    rm -rf ngless
