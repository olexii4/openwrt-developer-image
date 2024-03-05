FROM docker.io/debian:buster

# Install Node.js for che-code editor
ENV NODE_VERSION=v18.18.2
ENV NODE_DISTRO=linux-x64
ENV NODE_BASE_URL=https://nodejs.org/dist/${NODE_VERSION}

RUN curl -fsSL ${NODE_BASE_URL}/node-${NODE_VERSION}-${NODE_DISTRO}.tar.gz -o node-${NODE_VERSION}-${NODE_DISTRO}.tar.gz \
  && mkdir -p /usr/local/lib/nodejs \
  && tar -xzf node-${NODE_VERSION}-${NODE_DISTRO}.tar.gz -C /usr/local/lib/nodejs \
  && rm node-${NODE_VERSION}-${NODE_DISTRO}.tar.gz

ENV VSCODE_NODEJS_RUNTIME_DIR=/usr/local/lib/nodejs/node-${NODE_VERSION}-${NODE_DISTRO}/bin

# Install openwrt build dependencies
RUN apt-get update &&\
    apt-get install -y \
        sudo ccache time git-core subversion build-essential g++ bash make \
        libssl-dev patch libncurses5 libncurses5-dev zlib1g-dev gawk \
        flex gettext wget unzip xz-utils python python-distutils-extra \
        python3 python3-distutils-extra rsync curl libsnmp-dev liblzma-dev \
        libpam0g-dev cpio rsync re2c && \
    wget https://github.com/cli/cli/releases/download/v2.39.2/gh_2.39.2_linux_amd64.deb && \
    apt-get install -f ./gh_2.39.2_linux_amd64.deb && \
    apt-get clean && \
    useradd -m user && \
    echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user

# set dummy git config
RUN git config --global user.name "user" && git config --global user.email "user@example.com"