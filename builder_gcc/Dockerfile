# Dockerfile to build GCC on top of the builder image.

ARG GCC_VERSION=15.2.0
# Cores to use when building
ARG NUM_JOBS=4

# Stages: Do the build
FROM andrewdavidsmith/ubuntu-1604:latest AS builder-gcc-tmp

# Install GCC
# https://gcc.gnu.org/wiki/HomePage
# `make install-strip` generates a much smaller image
ARG GCC_VERSION
WORKDIR /tmp/gcc
RUN wget -nv https://gcc.gnu.org/pub/gcc/releases/gcc-${GCC_VERSION}/gcc-${GCC_VERSION}.tar.gz && \
    tar -zxf gcc-${GCC_VERSION}.tar.gz && \
    cd gcc-${GCC_VERSION} && \
    mkdir build && cd build && \
    ../configure \
    --enable-languages=c,c++ \
    --disable-multilib \
    --prefix=/usr/local \
    CFLAGS='-O2 -pipe' CXXFLAGS='-O2 -pipe' && \
    make -j${NUM_JOBS} && \
    make install-strip

# Stage 2: Create a small image
FROM andrewdavidsmith/ubuntu-1604:latest AS builder-gcc

COPY --from=builder-gcc-tmp /usr/local /usr/local
