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

RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config && \
    echo "PermitRootLogin no" >> /etc/ssh/sshd_config

RUN sed -i "s/#listen_addresses = 'localhost'/listen_addresses = '*'/" /etc/postgresql/*/main/postgresql.conf && \
    echo "host all all 0.0.0.0/0 scram-sha-256" >> /etc/postgresql/*/main/pg_hba.conf

EXPOSE 22
EXPOSE 5432

CMD service postgresql start && \
    /usr/sbin/sshd -D
