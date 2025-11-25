# Laboratorio Ansible & Docker

## Scopo del laboratorio
Questo laboratorio ha lo scopo di fornire un esempio pratico di utilizzo di Ansible per automatizzare la configurazione e la gestione di container Docker. Attraverso questo laboratorio, imparerai a creare playbook Ansible per distribuire e gestire applicazioni containerizzate.
In questo laboratorio verranno i container Docker verranno trattati come nodi gestiti da Ansible tramite connesseione SSH.

## Prerequisiti
- Ansible installato 
- Docker installato 
- Accesso SSH ai nodi Docker

## Struttura del progetto
- `hosts/inventory.ini`: File di inventario Ansible che elenca i nodi Docker.
- `playbooks/deploy.yml`: Playbook Ansible per deployare un'app nel container Docker.
- `node/Dockerfile`: File Dockerfile per creare l'immagine del nodo Docker.
- `controller/Dockerfile`: File Dockerfile per creare l'immagine del controller Ansible
- `docker-compose.yml`: File Docker Compose per definire e gestire i servizi Docker.
- `todo-app/`: Directory contenente il codice sorgente dell'applicazione PHP da eseguire nel container Docker.

## Esecuzione del laboratorio
1. Clona il repository del laboratorio:
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2. Controlla il file `hosts/inventory.ini` e aggiorna gli indirizzi IP e le porte dei nodi Docker se necessario:
    ```ini
    [ubuntu_nodes]
    node1 ansible_host=<docker_node_1_ip> ansible_port=<docker_node_1_ssh_port> ansible_user=root ansible_password=rootpass ansible_python_interpreter=/usr/bin/python3
    node2 ansible_host=<docker_node_2_ip> ansible_port=<docker_node_2_ssh_port> ansible_user=root ansible_password=rootpass ansible_python_interpreter=/usr/bin/python3
    ```
3. Avvia i container Docker utilizzando Docker Compose:
    ```bash
    docker compose up -d --build
    ```
4. Entra nel container del controller Ansible:
    ```bash
    docker exec -it ansible_controller bash
    ```
5. Esegui il playbook Ansible per distribuire i container Docker:
    ```bash
    ansible-playbook -i hosts/inventory.ini playbooks/deploy.yml
    ```
6. Accesso all'applicazione PHP tramite il browser web utilizzando l'indirizzo IP del nodo Docker e la porta 8080:
    ```
    http://localhost:8080 (per il nodo1)
    http://localhost:8081 (per il nodo2)
    ```
7. Arresta i container Docker al termine del laboratorio:
    ```bash
    docker compose down
    ```

## Contenuto dei Playbook
`deploy.yml`:
- Aggiorna i pacchetti sul nodo con apt.(apt update && apt upgrade -y)
- Controlla e installa PHP e le estensioni necessarie. (php, php-sqlite3)
- Avvia il server PHP integrato per eseguire l'applicazione. (php -S localhost:8080)
