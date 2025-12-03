FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# Installazione pacchetti necessari al control node di Ansible
RUN apt-get update && apt-get install -y \
    ansible sshpass python3 \
    && rm -rf /var/lib/apt/lists/*

# Configurazione di Ansible (disabilita controllo host key per semplicità in ambiente di laboratorio)
RUN mkdir -p /etc/ansible && \
    echo "[defaults]\nhost_key_checking = False\n" > /etc/ansible/ansible.cfg

WORKDIR /etc/ansible

# keep container running
CMD ["tail", "-f", "/dev/null"] 