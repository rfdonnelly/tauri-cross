# Adapted from: https://github.com/tauri-apps/tauri/issues/1355#issuecomment-896434917

FROM centos:centos7.9.2009

# Install dependencies
RUN \
    yum install -y \
        # notice I'm using an old version of webkit. It works!
        webkitgtk4-devel \
        openssl-devel \
        curl \
        wget \
        squashfs-tools \
        gcc \
        gcc-c++ \
        make \
        file \
        librsvg2-devel

# Install NVM
RUN \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash \
    && source $HOME/.nvm/nvm.sh \
    && nvm install 14 --latest-npm \
    && nvm use node

# Install Rust
RUN \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# Install Tauri CLI
RUN \
    source $HOME/.cargo/env \
    # do not use downloaded packages of tauri - you must build it yourself in this environment for correct GLIBC version
    && cargo install tauri-cli --vers 1.0.4
    # NOTE: tauri-macros has nothing to install (no binaries) so this isn't needed
    # && cargo install tauri-macros --vers 1.0.4

ENV PATH=/root/.nvm/versions/node/v14.20.0/bin:$PATH
ENV PATH=/root/.cargo/bin:$PATH

# now instead you build your appimage like:
# cargo tauri build --debug --verbose
