# Setup Ansible
In questo laboratorio, verrà introdotto e approfondito l'uso del tool di automazione Ansible.

Di seguito sono riportate le istruzioni per configurare e utilizzare Ansible.

## Prerequisiti
Avere Ansible installato sulla macchina host.

L'installazione di Ansible è disponibile al seguente [link](https://docs.ansible.com/projects/ansible/latest/installation_guide/index.html).

Nel caso di sistemi basati su Debian/Ubuntu, è possibile installare Ansible eseguendo:
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

Per verificare l'installazione, eseguire:
```bash
ansible --version
```

## Struttura della directory ansible
- `hosts/`: Contiene i file di inventario Ansible per definire i nodi gestiti.
    - `inventory.ini`: Esempio di file di inventario in formato INI.
    - `inventory.yml`: Esempio di file di inventario in formato YAML.
- `playbooks/`: Contiene i playbook Ansible per automatizzare le attività sui nodi.
    - `update_system.yml`: Esempio di playbook per aggiornare i sistemi gestiti.
    - `deploy_todoApp.yml`: Esempio di playbook per distribuire un'applicazione Todo.
    - `template_example.yml`: Esempio di playbook che utilizza un template Jinja2.
    - `roles_example.yml`: Esempio di playbook che utilizza ruoli Ansible.
    - `asciiquarium.yml`: Esempio di playbook per installare e configurare Asciiquarium.
- `roles/`: Contiene i ruoli Ansible per organizzare le configurazioni e le attività.
    - `webserver/`: Esempio di ruolo per configurare un server web.
    - `database/`: Esempio di ruolo per configurare un database.
- `templates/`: Contiene i file di template Jinja2 utilizzati nei playbook
    - `template_example.j2`: Esempio di file di template Jinja2.
- `ansible.cfg`: File di configurazione di Ansible.
- `README.md`: Questo file di istruzioni.

## Comandi da eseguire
1. **Verificare la connettività con i nodi**: <br>
   Dal terminale, navigare nella directory `ansible/` e eseguire:
   ```bash
   ansible all -m ping -i hosts/inventory.ini
   ```
   L'output dovrebbe mostrare che tutti i nodi gestiti rispondono correttamente e sarà del tipo:
   ```json
    node1 | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    node2 | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    ```

2. **Eseguire un playbook**: <br>
   Per eseguire un playbook Ansible, utilizzare il comando:
   ```bash
   ansible-playbook -i hosts/inventory.ini playbooks/<nome_playbook>.yml
   ```
   e seguire l'esecuzione del playbook attraverso l'output nel terminale.

3. **Utilizzare i ruoli Ansible**: <br>
   Per eseguire un playbook che utilizza ruoli, utilizzare lo stesso comando di cui sopra, assicurandosi che il playbook faccia riferimento ai ruoli presenti nella directory `roles/`.

## Esercizi suggeriti
Di seguito sono riportati alcuni esercizi suggeriti per familiarizzare con moduli e playbook di Ansible:

1. Creare un playbook per creare un file di testo su tutti i nodi gestiti.
   - Obbiettivo: Verificare che il controller riesca a scrivere sui nodi gestiti.
   - Moduli suggeriti: `file`, `copy`.
   - Links alla documentazione: 
     - [file module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/file_module.html)
     - [copy module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/copy_module.html)
2. Creare un playbook per creare un utente su tutti i nodi gestiti.
    - Obbiettivo: Verificare la gestione degli utenti sui nodi gestiti.
    - Moduli suggeriti: `user`.
    - Links alla documentazione: 
      - [user module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/user_module.html)
3. Creare un playbook per cambiare la password di un utente su tutti i nodi gestiti.
    - Obbiettivo: Verificare la gestione delle password sui nodi gestiti.
    - Moduli suggeriti: `user`.
    - Suggerimento: Utilizzare il filtro `password_hash` per generare una password crittografata.
4. Creare un playbook per installare un pacchetto software su tutti i nodi gestiti.
    - Obbiettivo: Familiarizzare con la gestione dei pacchetti tramite Ansible.
    - Moduli suggeriti: `apt` (per sistemi basati su Debian/Ubuntu)
    - Esempio: Installare `nginx` e `curl` su tutti i nodi gestiti.
    - Links alla documentazione:
      - [apt module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/apt_module.html)
5. Creare un playbook per avviare, arrestare e riavviare un servizio su tutti i nodi gestiti.
    - Obbiettivo: Gestire i servizi sui nodi gestiti.
    - Moduli suggeriti: `service`.
    - Esempio con `nginx`: 
        - Avviare il servizio: `state: started`
        - Arrestare il servizio: `state: stopped`
        - Riavviare il servizio: `state: restarted`
    - Links alla documentazione:
      - [service module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/service_module.html)

## Ulteriori esercizi avanzati
6. Copiare una directory intera su tutti i nodi gestiti.
    - Moduli suggeriti: `copy` con l'opzione `recursive: yes`.

7. Utilizzare un template Jinja2
    - Creare un file `.j2` nella directory `templates/`.
    - Utilizzare il modulo `template` per copiare il file template sui nodi gestiti, sostituendo le variabili definite.
    - Esempio: Creare un file di configurazione personalizzato per un'applicazione.
    - Links alla documentazione:
      - [template module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/template_module.html)
      - [Jinja2 templating](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_templating.html)

8. Eseguire un comando e salvare l'output
    - Usa il modulo `command` o `shell`.
    - Registra l'output con `register` e visualizzalo con il modulo `debug`.
    - Links alla documentazione:
      - [command module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/command_module.html)
      - [shell module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/shell_module.html)
      - [debug module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/debug_module.html)

9. Creare un playbook con più "play" separati. Ad esempio:
    - `Play 1`: Aggiornare i pacchetti sui nodi gestiti.
    - `Play 2`: Installare un'applicazione specifica.

10. Creare un ruolo Ansible personalizzato
    - Obbiettivo: Familiarizzare con la creazione e l'uso dei ruoli in Ansible.
    - Strutturare il ruolo con le directory standard (`tasks/`, `handlers/`, `templates/`, `files/`, ecc.).
    - Utilizzare il ruolo in un playbook.
    - Links alla documentazione:
      - [Ansible Roles](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

### Ritorna al [README principale](../README.md)