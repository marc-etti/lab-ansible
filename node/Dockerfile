FROM ubuntu:24.04
ENV DEBIAN_FRONTEND=noninteractive

# Installazione pacchetti necessari (Python per Ansible + OpenSSH server)
RUN apt-get update && \
    apt-get install -y python3 python3-apt apt-utils \
    openssh-server && \
    rm -rf /var/lib/apt/lists/*

# Creazione directory obbligatoria per SSH
RUN mkdir -p /var/run/sshd

# Imposta una password per l'utente root (solo per ambiente di laboratorio!)
RUN echo "root:rootpass" | chpasswd

# Consenti login root via password (bloccato di default)
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Evita disconnessioni con sessioni Docker
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

# Espone la porta SSH e la porta del server web
EXPOSE 22
EXPOSE 8080

# Copia la cartella dell'app todo-app nella directory web server
COPY ./todo-app /var/www/todo-app

# Avvia SSHD in foreground (necessario in Docker)
CMD ["/usr/sbin/sshd", "-D"]
