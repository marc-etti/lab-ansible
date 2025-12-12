# Laboratorio Ansible & Docker

## Scopo del laboratorio
Questo laboratorio ha lo scopo di fornire un esempio pratico di utilizzo di Ansible per automatizzare la configurazione e la gestione di container Docker. Attraverso questo laboratorio, imparerai a creare playbook Ansible per distribuire e gestire applicazioni containerizzate.
In questo laboratorio verranno i container Docker verranno trattati come nodi gestiti da Ansible tramite connesseione SSH.

## Prerequisiti
- **Ansible installato** <br>
    Verificabile attraverso il comando:
    ```bash
    ansible --version
    ```
- **Docker installato** <br>
    Verificabile attraverso il comando:
    ```bash
    docker --version
    ```
- **Accesso SSH ai nodi Docker** <br>
    Assicurarsi che il controller Ansible possa connettersi ai nodi Docker tramite SSH senza password (utilizzando chiavi SSH).

## Struttura del progetto
- `ansible/`: Directory contenente i playbook Ansible, i file di inventario e le configurazioni.
    - Link al [README di Ansible](ansible/README.md) per ulteriori dettagli.
- `docker/`: Directory contenente i file Docker Compose per avviare i container Docker necessari per il laboratorio.
    - Link al [README di Docker](docker/README.md) per ulteriori dettagli.
- `README.md`: Questo file di istruzioni.
- `.gitignore`: File per escludere file e directory non necessari dal controllo di versione.

## Esecuzione del laboratorio
1. Aprire un terminale all' interno della directory dove si vuole clonare il repository del laboratorio.

2. Clonare il repository del laboratorio:
    ```bash
    git clone <repository-url>
    ```
3. Navigare nella directory del laboratorio:
    ```bash
    cd lab-ansible/
    ```
4. Avviare i container Docker necessari per il laboratorio. Maggiori dettagli sono disponibili in `docker/README.md`.
    ```bash
    docker compose -f docker/docker-compose.yml up -d --build --force-recreate
    ```
4. Passare alle istruzione del laboratorio Ansible in `ansible/README.md` per eseguire i playbook Ansible sui nodi Docker.
5. Terminato il laboratorio, arrestare i container Docker. Aprire il terminale all'interno della directory `docker/`, ed eseguire:
    ```bash
    docker compose down
    ```
