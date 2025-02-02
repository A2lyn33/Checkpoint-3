# Exercice 2 : Manipulations pratiques sur VM Linux
>Pour cet exercice tu as besoin de la VM SRVLX01.
>> Pas de Sudo si connexion en "Root"
---
## Partie 1 : Gestion des utilisateurs<br>
---
### Q.2.1.1 Sur le serveur, créer un compte pour ton usage personnel.
  - Utilisation de la commande `adduser`
  - Création du _**Compte Adlyne**_ <br> 
![Capture d’écran 2025-01-17 120234](https://github.com/user-attachments/assets/7969838a-68a6-4bde-97c5-2d47147277c6)  

### Q.2.1.2 Quelles préconisations proposes-tu concernant ce compte ?
  - Utiliser un mot de passe fort.
  - Avoir des droits d'accès avec
    ```sudo```
  - Connexion SSH par clé et non par MDP.
---
## Partie 2 : Configuration de SSH

>Un serveur SSH est lancé sur le port par défaut.
>Il est possible de s'y connecter avec n'importe quel compte, y compris le compte root.
**Bien rédémarrer service ssh avec la commande ```sudo systemctl restart ssh``` après chaque modification <br>
---
### Q.2.2.1 Désactiver complètement l'accès à distance de l'utilisateur root.

![Capture d’écran 2025-01-17 121725](https://github.com/user-attachments/assets/45324c4c-5892-4938-9ea8-fe823d543703)

### Q.2.2.2 Autoriser l'accès à distance à ton compte personnel uniquement.<br> 
![Capture d’écran 2025-01-17 123212](https://github.com/user-attachments/assets/f49a430e-bc07-44f3-98a2-be801322c875)

### Q.2.2.3 Mettre en place une authentification par clé valide et désactiver l'authentification par mot de passe
![Capture d’écran 2025-01-17 124819](https://github.com/user-attachments/assets/4287d251-92ef-4ea8-91f8-df4b834d7b49)
![Capture d’écran 2025-01-17 125523](https://github.com/user-attachments/assets/86c5a73c-f0a7-47dc-9ae7-b0c2db19e0b4)

---
## Partie 3 : Analyse du stockage
---
### Q.2.3.1 Quels sont les systèmes de fichiers actuellement montés ?
Il y a :
  - ext2
  - ext4
### Q.2.3.2 Quel type de système de stockage ils utilisent ?
Il y a : <br> 
  - lvm
  - raid1

### Q.2.3.3 Ajouter un nouveau disque de 8,00 Gio au serveur et réparer le volume RAID
  - Rajout du Disque sur la VM : <br>
![Capture d’écran 2025-01-17 131655](https://github.com/user-attachments/assets/418a5cc0-5cd4-45be-a703-3a4d6eed06ab)
![Capture d’écran 2025-01-17 131716](https://github.com/user-attachments/assets/b0fd9b7e-803d-4787-9f43-cd6b2502eef7)
  - Création de la partition du disque SDB :
      - Utilisation de la commande : `fdisk /dev/sdb`
![Capture d’écran 2025-02-02 162633](https://github.com/user-attachments/assets/4d8d2192-3976-4b62-8134-7d4be0fa564f)
  - Réparer le RAID <br> 
      - Utilisation de la commande : `mdadm --add /dev/md0 /dev/sdb1`<br>
![Capture d’écran 2025-02-02 164427](https://github.com/user-attachments/assets/1d45b94c-7363-4a5b-b9c5-6707350e00ed)

### Q.2.3.4 Ajouter un nouveau volume logique LVM de 2 Gio qui servira à héberger des sauvegardes.<br>
> **Ce volume doit être monté automatiquement à chaque démarrage dans l'emplacement par défaut : /var/lib/bareos/storage.**
  - Voir les VGs disponible avec la commande : vgdisplay, puis créer un LV sur le groupe disponible via la commande : `lvcreate -L 2G -n Saves cp3-vg` <br>
![Capture d’écran 2025-02-02 165030](https://github.com/user-attachments/assets/abaad711-9f2e-4cce-9a9f-55854c1a79b9)
![Capture d’écran 2025-02-02 165315](https://github.com/user-attachments/assets/1c6e438a-ca2a-4b03-a18b-c5b5e840cad7)
  - On monte le LV via cette commande : `mount /dev/cp3-vg/Saves /var/lib/bareos/storage/`<br> 
![Capture d’écran 2025-02-02 165441](https://github.com/user-attachments/assets/6eafa39e-d5d9-45e5-8131-b81698cee4b6)
  - On configure le fichier `nano /etc/fstab`
![Capture d’écran 2025-02-02 165601](https://github.com/user-attachments/assets/d7576d12-dc18-43f5-91e0-caec16a0e025)

### Q.2.3.5 Combien d'espace disponible reste-t-il dans le groupe de volume ?
![Capture d’écran 2025-02-02 165711](https://github.com/user-attachments/assets/c82847e7-c9a3-4adc-bcbc-f27457da4a5f)

---
# Partie 4 : Sauvegardes
---
>Le logiciel bareos est installé sur le serveur.
>Les composants bareos-dir, bareos-sd et bareos-fd sont installés avec une configuration par défaut.

### Q.2.4.1 Expliquer succinctement les rôles respectifs des 3 composants bareos installés sur la VM.

  - bareos-dir (Director) : Coordonne les sauvegardes, récupérations et tâches de gestion.
  - bareos-sd (Storage Daemon) : Gère le stockage et le transfert des données vers les médias.
  - bareos-fd (File Daemon) : Installe sur les machines à sauvegarder pour transmettre les données au bareos-sd.

---

# Partie 5 : Filtrage et analyse réseau
---
### Q.2.5.1 Quelles sont actuellement les règles appliquées sur Netfilter ?
![Capture d’écran 2025-02-02 171239](https://github.com/user-attachments/assets/e4ffb3ad-b162-4859-8484-88fe93e7ed1c)

### Q.2.5.2 Quels types de communications sont autorisées ?<br> 
  - `ct state established, related accept` : les retours de connexions déjà établies.

  - `iifname "lo" accept` autorise le trafic local.

  - `TCP dport 22 accept` autorise les connexions TCP destinées au port 22 (port SSH).

  - `IP protocol icmp accept` autorise les pings IPV4.

  - `IP6 nexthdr icmpv6 accept` autorise les pings IPV6.

### Q.2.5.3 Quels types sont interdit ?
  - `ct state invalid drop` : les paquets ne pouvant pas être identifiés à une requêtes.<br>
> Et tout le reste qui n'est pas en accept.<br>

### Q.2.5.4 Sur nftables, ajouter les règles nécessaires pour autoriser bareos à communiquer avec les clients bareos potentiellement présents sur l'ensemble des machines du réseau local sur lequel se trouve le serveur.
  - Utilisation de la commande : `nft add rule inet inet_filter_table in_chain tcp dport { 9101-9103 } ct state new accept`
![Capture d’écran 2025-02-02 172146](https://github.com/user-attachments/assets/9f62de05-5802-4f37-95ab-ea2de30fd41e)
---
## Partie 6 : Analyse de logs
---
### Q.2.6.1 Lister les 10 derniers échecs de connexion ayant eu lieu sur le serveur en indiquant pour chacun :
> Aucun échec 
![Capture d’écran 2025-02-02 172850](https://github.com/user-attachments/assets/6a90f535-6c02-4ab5-b825-346d90a32b8f)

La date et l'heure de la tentative
L'adresse IP de la machine ayant fait la tentative
