#  Esercizi suggeriti
Di seguito sono riportati alcuni esercizi suggeriti per familiarizzare con moduli e playbook di Ansible:

1. Creare un playbook per creare un file di testo su tutti i nodi gestiti.
   - Obiettivo: Verificare che il controller riesca a scrivere sui nodi gestiti.
   - Moduli suggeriti: `file`, `copy`.
   - Links alla documentazione: 
     - [file module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/file_module.html)
     - [copy module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/copy_module.html)
2. Creare un playbook per creare un utente su tutti i nodi gestiti.
    - Obiettivo: Verificare la gestione degli utenti sui nodi gestiti.
    - Moduli suggeriti: `user`.
    - Links alla documentazione: 
      - [user module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/user_module.html)
3. Creare un playbook per cambiare la password di un utente su tutti i nodi gestiti.
    - Obiettivo: Verificare la gestione delle password sui nodi gestiti.
    - Installare la libreria `python3-passlib` sull'host Ansible se non è già presente con: `sudo apt install python3-passlib`.
    - Moduli suggeriti: `user`.
    - Suggerimento: Utilizzare il filtro `password_hash` per generare una password crittografata.
4. Creare un playbook per installare un pacchetto software su tutti i nodi gestiti.
    - Obiettivo: Familiarizzare con la gestione dei pacchetti tramite Ansible.
    - Moduli suggeriti: `apt` (per sistemi basati su Debian/Ubuntu)
    - Esempio: Installare `nginx` e `curl` su tutti i nodi gestiti.
    - Links alla documentazione:
      - [apt module](https://docs.ansible.com/projects/ansible/latest/collections/ansible/builtin/apt_module.html)
5. Creare un playbook per avviare, arrestare e riavviare un servizio su tutti i nodi gestiti.
    - Obiettivo: Gestire i servizi sui nodi gestiti.
    - Moduli suggeriti: `service`.
    - Esempio con `nginx`: 
        - Avviare il servizio: `state: started`
        - Arrestare il servizio: `state: stopped`
        - Riavviare il servizio: `state: restarted`
    - N.B. Se è ancora in esecuzione apache2, riavviare i nodi per liberare la porta 80, dopodiché rieseguire il playbook che installa e gestisce nginx prima di eseguire questo esercizio.
    - Per riavviare i nodi, aprire il terminale nella cartella `ansible/docker/` ed eseguire:
      ```
      docker compose down && docker compose up -d
      ```
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
    - Obiettivo: Familiarizzare con la creazione e l'uso dei ruoli in Ansible.
    - Strutturare il ruolo con le directory standard (`tasks/`, `handlers/`, `templates/`, `files/`, ecc.).
    - Utilizzare il ruolo in un playbook.
    - Links alla documentazione:
      - [Ansible Roles](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

### Ritorna al [README principale](../README.md)