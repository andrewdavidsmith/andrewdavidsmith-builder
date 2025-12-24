# Dockerfile to build the final builder image.

# Cores to use when building
ARG NUM_JOBS=4

FROM andrewdavidsmith/builder-cmake:latest AS builder-cmake
FROM andrewdavidsmith/builder-gcc:latest AS builder-gcc

FROM andrewdavidsmith/ubuntu-1604:latest AS builder

# Install dependencies
#
# binutils: need 'as' (the assembler)
# libc6-dev: basic headers in a sensible place
# libisl-dev and libmpc-dev: compiler won't work without these
# git and ca-certificates: needed for git clone
# make: needed by cmake for better debugging than ninja
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    make \
    binutils \
    libc6-dev \
    libisl-dev \
    libmpc-dev \
    git

# Need this: export LD_LIBRARY_PATH=/usr/local/lib64
# export LD_LIBRARY_PATH=/usr/local/lib
COPY --from=builder-cmake /usr/local/ /usr/local/
COPY --from=builder-gcc /usr/local/ /usr/local/
