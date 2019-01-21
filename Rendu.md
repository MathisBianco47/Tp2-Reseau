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


Adresse de réseau de la carte WiFi : 10.33.0.0

Adresse de broadcast de la carte WiFi : 10.33.3.255/22 =>  00001010.00100001.00000011.11111111
