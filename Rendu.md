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
Après 2h passé à essayer de faire la commande nc -l -p 8888, sur le mac de mathis,ainsi que celui de fred, nous n'avons réussi à faire le chat. Nous ne pouvons pas configurer l'ip 182.168.1.12 sur l'adaptateur réseau Nous ne pouvons qu'écouter mais pas envoyer de message. Nous avons essayé sur une VM Linux, évidemment cela n'a pas marché.   ### 6. WireShark On a pas forcement tout compris de ce truc, mais je te joins un screen des connexions que j'ai filtrer, meme si je vois pas l'interet.

---

### 6. Wireshark
![alt text]()

---

### 7. Firewall
...


## III. Manipulation d'autres outils/protocoles côté client

### DHCP 
La commande qui m'a permis de trouver le DHCP `system_profiler SPNetworkDataType | grep "Server Identifier"` (beaucoup de temps perdue)

`Serveur DHCP  : 10.33.3.254`

Avec cette commande, on ne peut pas obtenir la durée, ou on obtient `duration Osec`

---

**Ce que nous avons compris du DHCP**


Il est chargé de la configuration automatique des adresses IP d'un réseau. 
Cela évite à l'utilisateur de tout paramétrer ces IP manuellement.

---

**Demandez une nouvelle adresse IP**


on tape la commande `sudo ipconfig set en0 DHCP`

---

### DNS


Toujours avec la commande `system_profiler SPNetworkDataType`
on possède deux adresses dns, j'ai pris l'une des deux
`Serveur DNS : 10.33.10.20`

---

**Nslookup**

dig google.com :
```
;; ANSWER SECTION:
google.com.		41	IN	A	172.217.19.238

```
dig ynov.com :
```
;; ANSWER SECTION:
ynov.com.		1546	IN	A	217.70.184.38

```

---

**Reverse lookup**
Commande effectué: dig -x 78.78.21.21 +short
Premiere adresse : host-78-78-21-21.mobileonline.telia.com.

Commande effectué: dig -x 92.16.54.88 +short
Seconde adresse : host-92-16-54-88.as13285.net.

C'est la même chose que pour le lookup mais dans l'autre sens. C'est-à-dire que `78.78.21.21` est lié au nom de domaine host-78-78-21-21.mobileonline.telia.com

### 3. Bonus

**Se renseigner sur les différences entre WiFi et câble**

Le câble a un meilleur débit que la Wifi car il y a très peu de perte, car le signal ne peut être alterner par les mûrs 'exemple'

---

**explorer l'interface d'administration de votre box (chez vous) avec tout ça en tête**

C'est celle de Orange. 
L'interface est accessible via l'adresse ,
Sur ce site il y a la WIFI et l'IP etc.

---

**sinon, elle sert à quoi la MAC si on a des IP ? => Se renseigner sur ARP**

Une adresse IP est attribuée en fonction du réseau et peut changer alors que l'adresse MAC est physique en fonction de la carte réseau.

Nous ne posssèdons pas de switch.

---
