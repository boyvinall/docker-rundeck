# Ubuntu 16.04 based, runs as rundeck user
# https://hub.docker.com/r/rundeck/rundeck/tags
FROM rundeck/rundeck:3.3.10

ENV ANSIBLE_HOST_KEY_CHECKING=false
ENV RDECK_BASE=/home/rundeck
ENV MANPATH=${MANPATH}:${RDECK_BASE}/docs/man
ENV PATH=${PATH}:${RDECK_BASE}/tools/bin

# install ansible
# base image already installed: curl, openjdk-8-jdk-headless, ssh-client, sudo, uuid-runtime, wget
# (see https://github.com/rundeck/rundeck/blob/master/docker/ubuntu-base/Dockerfile)
RUN sudo apt-get -y update \
    && sudo apt-get -y --no-install-recommends install ca-certificates python3-pip sshpass \
    && sudo -H pip3 --no-cache-dir install --upgrade pip setuptools \
    && sudo -H pip3 --no-cache-dir install ansible==2.9.10 \
    && sudo rm -rf /var/lib/apt/lists/*

# add locally built plugins
COPY --chown=rundeck:root \
    */build/libs/*.jar \
    */build/libs/*.zip \
    ${RDECK_BASE}/libext/
