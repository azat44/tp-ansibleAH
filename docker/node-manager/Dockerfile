FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    python3 \
    python3-pip \
    sshpass \
    openssh-client \
    git \
    curl \
    vim \
    nano \
    iputils-ping \
    net-tools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install ansible ansible-lint

RUN mkdir -p /playbooks /inventory /root/.ssh

RUN ssh-keygen -t rsa -b 4096 -f /root/.ssh/id_rsa -N ""

RUN echo "Host *\n\tStrictHostKeyChecking no\n\tUserKnownHostsFile=/dev/null" > /root/.ssh/config && \
    chmod 600 /root/.ssh/config

WORKDIR /playbooks

CMD ["tail", "-f", "/dev/null"]