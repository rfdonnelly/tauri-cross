FROM centos:centos7.3.1611

RUN yum install -y \
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
  # for scp transfer of build
  openssh-clients \
  openssh

RUN \
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash && \
. $HOME/.nvm/nvm.sh && \
nvm install 14 --latest-npm && \
nvm use node

RUN \
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

RUN \
. $HOME/.cargo/env && \
# do not use downloaded packages of tauri - you must build it yourself in this environment for correct GLIBC version
cargo install tauri-cli --vers 1.0.4
# tauri-macros has nothing to install (no binaries)
# cargo install tauri-macros --vers 1.0.4

RUN \
    yum install -y \
        librsvg2-devel

ENV PATH=/root/.nvm/versions/node/v14.20.0/bin:$PATH
ENV PATH=/root/.cargo/bin:$PATH

# now instead you build your appimage like:
# cargo tauri build --debug --verbose
