FROM ubuntu:24.04

RUN apt update && \
    apt install -y ansible rsync python3-pip && \
    rm -rf /var/lib/apt/lists/*

RUN ansible-galaxy collection install ansible.posix
RUN ansible-galaxy collection install community.general
