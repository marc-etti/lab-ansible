# Setup Docker
Per questo laboratorio, utilizziamo i container di Docker per simulare i nodi gestiti da Ansible.

Di seguito sono riportate le istruzioni per configurare e avviare i container Docker necessari.

## Prerequisiti
Avere Docker installato sulla macchina host.
L'installazione di Docker è disponibile al seguente [link](https://docs.docker.com/get-started/get-docker/).

Per verificare l'installazione, eseguire:
```bash
docker --version
```

## Struttura della directory docker
- `controller/`: Contiene il Dockerfile per il container del controller Ansible.
- `node/`: Contiene il Dockerfile per il container del nodo Docker.
- `resources/`: Contiene file aggiuntivi (es. todo-app) necessari per il laboratorio.
- `docker-compose.yml`: File Docker Compose per definire e gestire i servizi Docker.
- `README.md`: Questo file di istruzioni.

## Comandi da eseguire

1. **Costruire le immagini Docker**
   Dal terminale, navigare nella directory `docker/` e eseguire:
   ```bash
   docker compose build
   ```

2. **Avviare i container**
   Eseguire il comando seguente per avviare i container definiti in `docker-compose.yml`:
   ```bash
   docker compose up -d
   ```

3. **Verificare lo stato dei container**
   Per verificare che i container siano in esecuzione, eseguire:
   ```bash
   docker ps
   ```

4. **Accedere ai container**
   Per accedere al container del controller Ansible, eseguire:
   ```bash
   docker exec -it ansible-controller bash
   ```
    Per accedere a un container nodo, eseguire:
    ```bash
    docker exec -it node1 bash
    ```

5. **Arrestare i container**
   Per arrestare i container, eseguire:
   ```bash
   docker compose down
   ```

### Ritorna al [README principale](../README.md)