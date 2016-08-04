# This file describes basic development environment for Cloudway.

FROM debian:jessie

# add llvm repo
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 6084F3CF814B57C1CF12EFD515CF4D18AF4F7421 \
	|| apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 6084F3CF814B57C1CF12EFD515CF4D18AF4F7421
RUN echo deb http://llvm.org/apt/jessie/ llvm-toolchain-jessie-3.8 main > /etc/apt/sources.list.d/llvm.list

# Packaged dependencies
RUN apt-get clean && apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    automake \
    bash-completion \
    binutils-mingw-w64 \
    bsdmainutils \
    build-essential \
    clang-3.8 \
    createrepo \
    curl \
    dpkg-sig \
    gcc-mingw-w64 \
    git \
    libtool \
    mercurial \
    net-tools \
    pkg-config \
    python-dev \
    python-mock \
    python-pip \
    python-websocket \
    tar \
    zip \
    && ln -snf /usr/bin/clang-3.8 /usr/local/bin/clang \
    && ln -snf /usr/bin/clang++-3.8 /usr/local/bin/clang++

# Configure the container for OSX cross compilation
ENV OSX_SDK MacOSX10.11.sdk
ENV OSX_CROSS_COMMIT 8aa9b71a394905e6c5f4b59e2b97b87a004658a4
RUN set -x \
    && export OSXCROSS_PATH="/osxcross" \
    && git clone https://github.com/tpoechtrager/osxcross.git $OSXCROSS_PATH \
    && (cd $OSXCROSS_PATH && git checkout -q $OSX_CROSS_COMMIT) \
    && curl -sSL https://s3.dockerproject.org/darwin/v2/${OSX_SDK}.tar.xz -o "${OSXCROSS_PATH}/tarballs/${OSX_SDK}.tar.xz" \
    && UNATTENDED=yes OSX_VERSION_MIN=10.6 ${OSXCROSS_PATH}/build.sh
ENV PATH /osxcross/target/bin:$PATH

# Install Go
# IMPORTANT: If the version of Go is updated, the Windows to Linux CI machines
#            will need updating, to avoid errors.
ENV GO_VERSION 1.6.2
RUN curl -fsSL "https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz" \
    | tar -xzC /usr/local
ENV PATH /go/bin:/usr/local/go/bin:$PATH
