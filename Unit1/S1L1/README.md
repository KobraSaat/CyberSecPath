# Configurazione del Laboratorio Virtuale con Kali Linux e Metasploitable 2

## Introduzione
Questo esercizio guida alla creazione di un ambiente di laboratorio virtuale su VirtualBox, utilizzando **Kali Linux** e **Metasploitable 2**. Questo setup consente di testare vulnerabilità e praticare tecniche di penetration testing in un ambiente sicuro.

## Requisiti
Prima di iniziare, assicurati di avere:

- **VirtualBox 7.1.6** installato ([Scaricalo qui](https://www.virtualbox.org/))
- **Kali Linux VM** ([Scaricalo qui](https://www.kali.org/get-kali/#kali-virtual-machines))
- **Metasploitable 2 VM** ([Scaricalo qui](https://sourceforge.net/projects/metasploitable/))

# **1. Installazione di Kali Linux su VirtualBox**

## 1. Importare la VM in VirtualBox

1. Apri **VirtualBox**.
2. Clicca su **Macchina > Aggiungi...**.
![immagine](https://github.com/user-attachments/assets/4b38de1a-3616-4ffb-a595-7e095aa5d992)

4. Vai nella cartella dove hai estratto i file e seleziona il file `.vbox`.
![immagine](https://github.com/user-attachments/assets/9ff94fef-35e6-465f-9b87-5bb9bc853dd9)

6. Clicca su **Apri**.

---

## 2. Configurare la VM

1. Seleziona la macchina virtuale e clicca su **Impostazioni**.
2. Vai su **Sistema > Scheda Madre** e imposta almeno **4096 MB di RAM**.
![immagine](https://github.com/user-attachments/assets/05f56e9f-677b-4d7e-a961-e3c844129a71)

4. Vai su **Sistema > Processore** e aumenta il numero di CPU per migliori prestazioni. (Default 2)
![immagine](https://github.com/user-attachments/assets/35628a2d-7400-4918-90a5-39c2f1ef3fb9)

---

## 3. Configurazione della Rete

Dopo aver importato Kali, configura le interfacce di rete:

1. **Scheda 1 - NAT** → Per l'accesso a Internet.
![immagine](https://github.com/user-attachments/assets/93ca835c-4538-4971-9a2e-746f11e6d569)

3. **Scheda 2 - Rete Solo Host** → Per CTF con DHCP.
![immagine](https://github.com/user-attachments/assets/9e8f156b-f355-49fb-8d73-762b3c267ee8)

5. **Scheda 3 - Rete Interna** → Per comunicare con Metasploitable 2.
![immagine](https://github.com/user-attachments/assets/cf2c5176-fb78-4160-b7ed-0c0dd4ac6b51)

### Configurazione della Rete su Kali
## 4. Avviare Kali Linux

1. Seleziona la VM di Kali Linux.
2. Clicca su **Avvia**.
3. Alla schermata di login, usa le credenziali predefinite:
   - **Nome utente:** kali
   - **Password:** kali
2. Controlla le interfacce di rete con:
   ```bash
   ip a
   ```
![immagine](https://github.com/user-attachments/assets/f7cbcbd3-a1a9-4a13-b524-5e2095cce8f2)

---

## 5. Aggiornare il Sistema (Consigliato)

1. Apri un **terminale** all'interno di Kali Linux.
2. Esegui i seguenti comandi:
   ```bash
   sudo apt update && sudo apt upgrade -y
   
   ```
![immagine](https://github.com/user-attachments/assets/b7d88072-ab50-4481-ab4a-e3af07aeef41)


# Installazione di Metasploitable 2 

## 1. Creare una Nuova Macchina Virtuale

1. Apri **VirtualBox** e clicca su **Nuova**.
2. Imposta i seguenti parametri:
   - **Nome e Sistema operativo**
      - **Nome e :** Metasploitable2
      - **Tipo:** Linux
      - **Sottotipo:** Ubuntu
      - **Versione:** Ubuntu (32-bit)
        
   ![immagine](https://github.com/user-attachments/assets/20a37d9f-c8aa-4920-9413-1e0ab8d76d9e)

   - **Hardware:**
      - Memoria di base: Assegna **512 MB di RAM** (1024 MB consigliati).
      - Processori: 1
    
   ![immagine](https://github.com/user-attachments/assets/42c35f39-1242-49fb-93ec-c3376018c031)

   - **Disco Fisso:**
   - Seleziona **Usa un file di disco fisso virtuale esistente:**
      - Clicca su **scegliere un file di disco fisso virtuale.**
   ![immagine](https://github.com/user-attachments/assets/5a9daa89-cf78-41f8-9cdb-a28b83a98aaf)
      - clicca su aggiungi e seleziona il file .vmdk estratto all'interno della cartella Metasploitable 2, dopo di che clicca su **Scegli**.
   ![immagine](https://github.com/user-attachments/assets/563d6976-9228-4292-b5d9-7053d1e6f1d2)
   ![immagine](https://github.com/user-attachments/assets/dbfd64f4-66cc-4117-a75f-1f0c9650860f)

   

3. Clicca su **fine**

---

## 2. Configurazione della Rete

1. Vai su **Impostazioni > Rete**.
2. Configura la **Scheda 1** su **Rete Interna** per la comunicazione con Kali Linux.
![immagine](https://github.com/user-attachments/assets/26389989-0c41-4934-97c3-4af924c3cbec)


---

## 4. Avviare Metasploitable 2

1. Seleziona la VM e clicca su **Avvia**.
2. Quando richiesto, effettua l'accesso con:
   - **Nome utente:** msfadmin
   - **Password:** msfadmin

---

## 5.Impostare un IP Statico su Metasploitable 2

1. Accedi alla macchina virtuale con le credenziali:
   ```bash
   msfadmin:msfadmin
   ```
2. Apri il file delle configurazioni di rete:
   ```bash
   sudo nano /etc/network/interfaces
   ```
3. Modifica il file aggiungendo o modificando le seguenti righe con un la rete desiderata, poichè si tratta di rete interna non serve impostare il gateway:
   ```plaintext
   auto eth0
   iface eth0 inet static
   address 192.168.10.100
   netmask 255.255.255.0
   ```
![immagine](https://github.com/user-attachments/assets/a2db1e18-3956-4458-ac9e-8c49499d87c5)

4. Salva il file premendo **CTRL + o** e **Invio** e poi **CTRL + x** .
5. Riavvia la rete con:
   ```bash
    sudo /etc/init.d/networking restart
   ```
6. Verifica l'IP assegnato con:
   ```bash
   ip a
   ```
![immagine](https://github.com/user-attachments/assets/a3f461db-29d5-46b9-89ad-7b3bbc849fad)

---



   
