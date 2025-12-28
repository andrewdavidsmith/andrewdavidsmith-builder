# Dockerfile to build a recent CMake on the low GLIBC base.

ARG CMAKE_VERSION=4.1.2
# Cores to use when building
ARG NUM_JOBS=1

FROM andrewdavidsmith/ubuntu-1604:latest AS builder-cmake-tmp

# Install CMake
# https://cmake.org/cmake/help/book/mastering-cmake/index.html
# ENV PATH="/opt/binutils-${BINUTILS_VERSION}/bin:${PATH}"
ARG CMAKE_VERSION
WORKDIR /tmp/cmake
RUN export LD_LIBRARY_PATH=/usr/local/lib64 && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    liblzma-dev \
    libcurl4-openssl-dev && \
    wget -nv https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}.tar.gz && \
    tar -zxf cmake-${CMAKE_VERSION}.tar.gz && \
    cd cmake-${CMAKE_VERSION} && \
    ./bootstrap --parallel=${NUM_JOBS} --system-curl --system-bzip2 --system-liblzma --no-debugger --no-qt-gui --prefix=/usr/local && \
    make -j${NUM_JOBS} && \
    make install

# Stage 2: Create a small image
FROM andrewdavidsmith/ubuntu-1604:latest AS builder-cmake

COPY --from=builder-cmake-tmp /usr/local /usr/local
