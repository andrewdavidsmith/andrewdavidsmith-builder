# Dockerfile to build starting from as low a GLIBC as possible

# Cores to use when building
ARG NUM_JOBS=28

FROM ubuntu:16.04 AS ubuntu-1604

# Install package dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    autoconf \
    automake \
    ca-certificates \
    libssl-dev \
    libgmp-dev \
    libmpfr-dev \
    libisl-dev \
    libmpc-dev \
    wget \
    git \
    pkgconf \
    texinfo \
    && rm -rf /var/lib/apt/lists/*
