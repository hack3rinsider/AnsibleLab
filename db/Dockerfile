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

COPY schema.sql /tmp/schema.sql

EXPOSE 22
EXPOSE 5432

CMD sed -i "s/^#listen_addresses.*/listen_addresses = '*'/" /etc/postgresql/16/main/postgresql.conf && \
    grep -q "host all all 0.0.0.0/0 trust" /etc/postgresql/16/main/pg_hba.conf || echo "host all all 0.0.0.0/0 trust" >> /etc/postgresql/16/main/pg_hba.conf && \
    service postgresql start && \
    su - postgres -c "createdb bankingdb" || true && \
    su - postgres -c "psql -d bankingdb -f /tmp/schema.sql" && \
    /usr/sbin/sshd -D
