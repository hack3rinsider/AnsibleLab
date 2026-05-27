FROM node:22-bookworm

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
    openssh-server \
    sudo \
    curl \
    nano \
    net-tools \
    netcat-openbsd \
    nginx && \
    npm install -g pm2 && \
    apt-get clean

RUN useradd -m -s /bin/bash devops && \
    echo "devops:devops123" | chpasswd && \
    usermod -aG sudo devops

RUN mkdir /var/run/sshd

RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "PermitRootLogin no" >> /etc/ssh/sshd_config

EXPOSE 22
EXPOSE 80

CMD service nginx start && /usr/sbin/sshd -D
