# Configurazione del Laboratorio Virtuale con Kali Linux e Metasploitable 2

## Introduzione
Questo esercizio guida alla creazione di un ambiente di laboratorio virtuale su VirtualBox, utilizzando **Kali Linux** e **Metasploitable 2**. Questo setup consente di testare vulnerabilità e praticare tecniche di penetration testing in un ambiente sicuro.

## Requisiti
Prima di iniziare, assicurati di avere:

- **VirtualBox** installato ([Scaricalo qui](https://www.virtualbox.org/))
- **Kali Linux VM** ([Scaricalo qui](https://www.kali.org/get-kali/#kali-virtual-machines))
- **Metasploitable 2 VM** ([Scaricalo qui](https://sourceforge.net/projects/metasploitable/))

## **1. Installazione di Kali Linux su VirtualBox**

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
3. Configura manualmente la rete interna se necessario:
   ```bash
   sudo ip addr add 192.168.56.10/24 dev eth2
   ```
4. Controlla la connettività con Metasploitable:
   ```bash
   ping 192.168.56.100
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
