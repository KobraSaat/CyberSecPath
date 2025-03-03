# Configurazione del Laboratorio Virtuale con Kali Linux e Metasploitable 2

## Introduzione
Questo esercizio guida alla creazione di un ambiente di laboratorio virtuale su VirtualBox, utilizzando **Kali Linux** e **Metasploitable 2**. Questo setup consente di testare vulnerabilità e praticare tecniche di penetration testing in un ambiente sicuro.

## Requisiti
Prima di iniziare, assicurati di avere:

- **VirtualBox** installato ([Scaricalo qui](https://www.virtualbox.org/))
- **Kali Linux VM** ([Scaricalo qui](https://www.kali.org/get-kali/#kali-virtual-machines))
- **Metasploitable 2 VM** ([Scaricalo qui](https://sourceforge.net/projects/metasploitable/))

# **1. Installazione di Kali Linux su VirtualBox**

## 1. Importare la VM in VirtualBox

1. Apri **VirtualBox**.
2. Clicca su **Macchina > Aggiungi...**.
3. Vai nella cartella dove hai estratto i file e seleziona il file `.vbox`.
4. Clicca su **Apri**.

---

## 2. Configurare la VM

1. Seleziona la macchina virtuale e clicca su **Impostazioni**.
2. Vai su **Sistema > Scheda Madre** e imposta almeno **4096 MB di RAM**.
3. Vai su **Sistema > Processore** e aumenta il numero di CPU per migliori prestazioni. (Default 2)

---

## 3. Configurazione della Rete

Dopo aver importato Kali, configura le interfacce di rete:

1. **Scheda 1 - NAT** → Per l'accesso a Internet.
2. **Scheda 2 - Rete Solo Host** → Per CTF con DHCP.
3. **Scheda 3 - Rete Interna** → Per comunicare con Metasploitable 2.

### Configurazione della Rete su Kali
1. Avvia Kali e apri un terminale.
2. Controlla le interfacce di rete con:
   ```bash
   ip a
   ```
---

## 4. Avviare Kali Linux

1. Seleziona la VM di Kali Linux.
2. Clicca su **Avvia**.
3. Alla schermata di login, usa le credenziali predefinite:
   - **Nome utente:** kali
   - **Password:** kali

---

## 5. Aggiornare il Sistema (Consigliato)

1. Apri un **terminale** all'interno di Kali Linux.
2. Esegui i seguenti comandi:
   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

# Installazione di Metasploitable 2 

## 1. Creare una Nuova Macchina Virtuale

1. Apri **VirtualBox** e clicca su **Nuova**.
2. Imposta i seguenti parametri:
   - **Nome:** Metasploitable2
   - **Tipo:** Linux
   - **Versione:** Ubuntu (32-bit)
3. Assegna almeno **512 MB di RAM** (1024 MB consigliati).
4. Seleziona **Non aggiungere un disco virtuale** e clicca su **Crea**.

---

## 2. Aggiungere il Disco `.vmdk`

1. Seleziona la VM appena creata e clicca su **Impostazioni**.
2. Vai su **Archiviazione** e clicca su **Controller: IDE**.
3. Clicca su **Aggiungi disco esistente** e seleziona il file `.vmdk` estratto.
4. Conferma cliccando su **OK**.

---

## 3. Configurazione della Rete

1. Vai su **Impostazioni > Rete**.
2. Configura la **Scheda 1** su **Rete Interna** per la comunicazione con Kali Linux.

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
4. Salva il file premendo **CTRL + X**, poi **Y** e **Invio**.
5. Riavvia la rete con:
   ```bash
    sudo /etc/init.d/networking restart
   ```
6. Verifica l'IP assegnato con:
   ```bash
   ip a
   ```

---



   
