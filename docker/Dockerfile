FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash \
    build-essential \
    ca-certificates \
    clang \
    clang-format \
    curl \
    gcc-multilib \
    git \
    libcapstone-dev \
    make \
    binutils-mips-linux-gnu \
    python3 \
    python3-pip \
    ripgrep \
    tar \
    xz-utils \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /work

CMD ["bash"]
