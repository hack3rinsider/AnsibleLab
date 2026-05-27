FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    ansible \
    openssh-server \
    openssh-client \
    sshpass \
    iputils-ping \
    vim nano && \
    apt-get clean

RUN mkdir /var/run/sshd

RUN useradd -m -s /bin/bash devops && \
    echo "devops:devops123" | chpasswd && \
    usermod -aG sudo devops

RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "PermitRootLogin no" >> /etc/ssh/sshd_config

WORKDIR /ansible

CMD service ssh start && bash
