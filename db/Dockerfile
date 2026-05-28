FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    postgresql \
    postgresql-contrib \
    openssh-server \
    sudo \
    python3 \
    nano \
    net-tools \
    iputils-ping && \
    apt-get clean

RUN useradd -m -s /bin/bash devops && \
    echo "devops:devops123" | chpasswd && \
    usermod -aG sudo devops

RUN mkdir -p /var/run/sshd

RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "PermitRootLogin no" >> /etc/ssh/sshd_config

EXPOSE 22
EXPOSE 5432

CMD service postgresql start && /usr/sbin/sshd -D
