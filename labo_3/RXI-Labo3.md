# RXI - Labo 3 

[TOC]



## **Objectif 1 : Mise en place du réseau LAN**

> Quelle est la commande utilisée pour configurer l'adresse IP fixe sur PC1 ?**

```bash
sudo ip address add 10.1.1.2/24 dev ens3
```

> Quelle est la commande utilisée pour configurer l'adresse IP fixe sur PC2 ?**

```bash
sudo ip address add 10.1.1.3/24 dev ens3
```

> Expliquez, à l'aide d'un exemple, la signification des statistiques fournies par la commande ping (valeurs rtt, min, max, avg).**

Lorsqu'on exécute la commande `ping`, voici un exemple de sortie :

```bash
bashCopyEditping 10.1.1.3 -c 4
64 bytes from 10.1.1.3: icmp_seq=1 ttl=64 time=0.102 ms
64 bytes from 10.1.1.3: icmp_seq=2 ttl=64 time=0.094 ms
64 bytes from 10.1.1.3: icmp_seq=3 ttl=64 time=0.087 ms
64 bytes from 10.1.1.3: icmp_seq=4 ttl=64 time=0.091 ms

--- 10.1.1.3 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3025ms
rtt min/avg/max/mdev = 0.087/0.093/0.102/0.005 ms
```

- **rtt min** : Temps minimum de réponse (`0.087 ms` dans l'exemple).
- **rtt avg** : Temps moyen de réponse (`0.093 ms`).
- **rtt max** : Temps maximal de réponse (`0.102 ms`).
- **mdev** : Écart-type, qui indique la variation des temps de réponse (`0.005 ms`).

Un faible `rtt avg` signifie une bonne connexion avec peu de latence, tandis qu'un `mdev` élevé indique des variations importantes dans les temps de réponse, ce qui peut signaler un problème réseau.

## Objectif 2 : Configuration de base d’un routeur Cisco

> Que fait la commande Cisco `ip address 10.1.1.1 255.255.255.0` ?

Elle assigne l'adresse IP `10.1.1.1` avec le masque de sous-réseau `255.255.255.0` à l'interface active du routeur.

Exemple :

```bash
Cheseaux# ip address 10.1.1.1 255.255.255.0
```

Cela permet au routeur de communiquer sur le réseau `10.1.1.0/24`.

> Que fait la commande Cisco interface `ethernet0/0` ?

Elle permet d'entrer en mode de configuration de l’interface `ethernet0/0` du routeur.

Exemple :

```bash
Cheseaux# interface ethernet0/0
```

Toutes les commandes suivantes seront appliquées sur cette interface.

> Que fait la commande Cisco no shutdown ?

Elle active l'interface réseau (`ethernet0/0` dans ce cas), qui est désactivée par défaut.

Exemple :

```bash
Cheseaux# no shutdown
```

Une fois exécutée, l’interface devient opérationnelle et peut commencer à envoyer et recevoir des paquets.

## Objectif 3 : Configuration de DHCP

>Sur le routeur "Cheseaux", quittez le mode "Configuration" avec la commande exit. Vous devriez être en mode "Enable", donc avec le prompt: "Cheseaux#".
>
>Puis utilisez la commande show running-config pour afficher la configuration.
>
>Insérez, comme réponse, les lignes qui montrent votre configuration DHCP.

Après avoir exécuté la commande `show running-config` en mode **Enable** (`Cheseaux#`), les lignes pertinentes concernant DHCP ressemblent à ceci :

```bash
ip dhcp pool cheseaux_sr1
   network 10.1.1.0 255.255.255.0
   default-router 10.1.1.1
   lease 1
```

Ces lignes indiquent :

1. Le **nom du pool DHCP** (`cheseaux_sr1`).
2. Le **réseau concerné** (`10.1.1.0/24`).
3. Le **routeur par défaut** (`10.1.1.1`).
4. La **durée du bail** (`1 jour`)

> Que fait la commande Cisco `ip dhcp pool ...` ?

Elle crée un **pool DHCP** qui attribue dynamiquement des adresses IP aux appareils du réseau.

Exemple :

```bash
Cheseaux# ip dhcp pool cheseaux_sr1
```

Cela permet d'entrer dans le mode de configuration du pool DHCP nommé `cheseaux_sr1`.

> Que fait la commande Cisco `network ... ...` avec le pool DHCP créé précédemment ?**

Elle définit la plage d'adresses IP qui seront attribuées par le serveur DHCP.

Exemple :

```bash
Cheseaux# network 10.1.1.0 255.255.255.0
```

Cela signifie que le serveur DHCP va distribuer des adresses **dans le sous-réseau 10.1.1.0/24**.

> Que fait la commande Cisco `lease 1` ?**

Elle définit la **durée du bail DHCP**.

Exemple :

```bash
Cheseaux# lease 1
```

Cela signifie que chaque adresse IP attribuée sera **valide pendant 1 jour** avant qu’un renouvellement ne soit nécessaire.

> Quelle est la commande pour effacer l'adresse IP fixe sur PC1 ?**

```bash
sudo ip address del 10.1.1.2/24 dev ens3
```

Cela supprime l'adresse IP `10.1.1.2` de l'interface `ens3`.

> Dans le fichier `/etc/network/interfaces`, quelle est la ligne qui active DHCP sur l'interface ens3 ?**

```bash
iface ens3 inet dhcp
```

Cette ligne indique que l'interface `ens3` doit obtenir une adresse IP **dynamiquement** via DHCP.

## Objectif 4 : Analyse de DHCP

>Téléchargez le diagramme en flèche de la capture DHCP. Le diagramme doit indiquer
>
>1. le type de chaque paquet
>2. les adresses IP source et destination

> Expliquez le but de chacun des messages DHCP échangés.

> Décrivez 3 des options que le serveur DHCP annonce au PC dans son message "Offer". 



## Objectif 5 : Sauvegarde de la configuration

## Objectif 6 : Utilisation de Netcat