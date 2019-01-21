BIANCO Mathis
# TP2-Reseau
Ce tp est entièrement réalisé sous le système macOs.

## I. Exploration locale en solo


### 1. Affichage d'informations sur la pile TCP/IP locale


---
Affichez les infos des cartes réseau sur mac :

Sur mac, on ouvre bash et on tape la commande ifconfig

| NOM         | Carte Réseau Sans Fil           | Binaire|
| ------------- |-------------|----------------|
| Masque de sous-réseau      | 0xfffffc00 ou 255.255.252.0 | 11111111.11111111.11111100.00000000|
| Adresse MAC      | f0:18:98:29:6b:81 ||
| Adresse IP (IPv4) | 10.33.3.14      |00001010.00100001.00000011.00001110|


**Nous ne possèdons pas de carte ethernet !**


Adresse de réseau de la carte WiFi : `10.33.0.0`

Adresse de broadcast de la carte WiFi : `10.33.3.255/22` =>  00001010.00100001.00000011.11111111

---
**Affichez votre gateway**

On peut obtenir ce genre d'informations avec la commande `route -n get default`.

Passerelle par défaut : `10.33.3.253`


---
**GUI - Trouvez comment afficher les informations sur une carte IP (change selon l'OS) :**


+ Clic droit sur la touche option puis sur *WI-FI* du bureau,
   + *Ouvrir les préférences Réseau et Internet*
+ Clic sur *avancé* 
+ Clic sur onglet sur *TCP/IP*

---
**A quoi sert la gateway dans le réseau d'Ingésup ?**

Le gateway est l'adresse qui permet de communiquer avec internet.

---
**Calculez la première et la dernière IP disponibles du réseau :**

Première adresse IP disponible est `10.33.3.1`                                                                          Dernière adresse IP disponible est `10.33.3.255`

---
**Nmap :**

Aprés l'installation de Nmap, j'ai tapé la commande `nmap -sn -PE 10.33.0.0/22`

```
Nmap scan report for 10.33.3.254
Host is up (0.0055s latency).
Nmap done: 1024 IP addresses (85 hosts up) scanned in 28.75 seconds
MAC Address: F4:BF:80:C0:A5:8A (Unknown)

```
On remarque qu'il y a 1024 adresses IP dans le réseau.

---

## II. Exploration locale en duo

### 1. Prérequis

+ On a un cable RJ45
+ On a désactivé nos deux firewalls

### 2. Cablâge

branché via le port Ethernet à nos adapteurs.

---

### 3. Modification d'adresse IP


Nous avons tout deux modifié l'adresse IP de notre carte Ethernet

Adresse IP de Sallès Sascha : `10.0.0.2`

Adresse IP de Bianco Mathis : `10.0.0.3`

Masque de sous-réseau : `255.255.255.0`

---

**Test avec le ping :**

```
--- 10.0.0.2 ping statistics ---
9 packets transmitted, 9 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 0.553/0.877/1.108/0.172 ms
MacBook-Pro-de-Mathis:~ mathisbianco$ 
```
---

### 4. Utilisation d'un des deux comme gateway

Mathis désactive sa carte Wifi et n'a plus accès à internet.

J'active, sur ma carte Wifi 

---

### 5. Petit chat privé


---

### 6. Wireshark
![alt text]()

---

### 7. Firewall


