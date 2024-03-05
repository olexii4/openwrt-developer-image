FROM registry.access.redhat.com/ubi9/python-39:1-165

# Switching to root user (setting UID to 0)
USER 0

RUN dnf -y update
RUN dnf -y install bash-completion bzip2 gcc gcc-c++ git make cmake ncurses-devel patch
RUN dnf -y install  rsync tar unzip wget which diffutils perl && \
    dnf -y clean all --enablerepo='*'
