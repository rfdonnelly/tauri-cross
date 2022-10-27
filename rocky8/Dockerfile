# Adapted from: https://github.com/tauri-apps/tauri/issues/1355#issuecomment-896434917

ARG ROCKY_VERSION=8.6
FROM rockylinux:$ROCKY_VERSION

ARG NVM_VERSION=0.39.2
ARG NODE_VERSION=16.18.0
ARG TAURI_VERSION=1.1.1

# Install dependencies
RUN \
    yum install -y \
        webkit2gtk3-devel \
        libappindicator-gtk3-devel \
        openssl-devel \
        curl \
        wget \
        squashfs-tools \
        gcc \
        gcc-c++ \
        make \
        file \
        librsvg2-devel

# Provides `find` for `nvm use node`
RUN \
    yum install -y \
        findutils

RUN useradd -u 1000 docker
USER docker
ENV HOME=/home/docker

# Install NVM
RUN \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v$NVM_VERSION/install.sh | bash \
    && env \
    && source $HOME/.nvm/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm use node

# Install Rust
RUN \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

ENV PATH=$HOME/.nvm/versions/node/v$NODE_VERSION/bin:$PATH
ENV PATH=$HOME/.cargo/bin:$PATH

# Install Tauri CLI
RUN \
    # do not use downloaded packages of tauri - you must build it yourself in this environment for correct GLIBC version
    cargo install tauri-cli --version $TAURI_VERSION

# now instead you build your appimage like:
# cargo tauri build --debug --verbose
