FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    openssh-server \
    python3 \
    sudo \
    curl \
    iputils-ping \
    net-tools \
    ca-certificates \
    apt-transport-https \
    gnupg \
    lsb-release \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/run/sshd && \
    echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

RUN useradd -m -s /bin/bash ubuntu && \
    echo "ubuntu:ubuntu" | chpasswd && \
    echo "ubuntu ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ubuntu

RUN mkdir -p /var/opt/gitlab /var/log/gitlab /etc/gitlab && \
    chown -R ubuntu:ubuntu /var/opt/gitlab /var/log/gitlab /etc/gitlab

RUN mkdir -p /home/ubuntu/.ssh && \
    chmod 700 /home/ubuntu/.ssh && \
    chown ubuntu:ubuntu /home/ubuntu/.ssh

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]