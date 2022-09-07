Module-4: Gestion des réseaux

 1. Les différents types de réseaux
	 
	 1. Le réseau de type **BRIDGE**

Tout d'abord, lorsque vous installez Docker pour la première fois, il crée automatiquement un réseau bridge nommé  **bridge**  connecté à l'interface réseau  **docker0**  ( consultable avec la commande  ip addr show docker0  ). Chaque nouveau conteneur Docker est automatiquement connecté à ce réseau, sauf si un réseau personnalisé est spécifié.

Par ailleurs,  **le réseau bridge est le type de réseau le plus couramment utilisé**. Il est limité aux conteneurs d'un hôte unique exécutant le moteur Docker. Les conteneurs qui utilisent ce driver, ne peuvent communiquer qu'entre eux, cependant ils ne sont pas accessibles depuis l'extérieur. 
![Docker bridge network](https://devopssec.fr/images/articles/docker/networks/bridge_network_docker.jpg)
Pour que les conteneurs sur le réseau bridge puissent communiquer ou être accessibles du monde extérieur, vous devez configurer le mappage de port.

2. Le réseau de type **HOST**
Ce type de réseau permet aux conteneurs d'utiliser la même interface que l'hôte. Il supprime donc l'isolation réseau entre les conteneurs et seront par défaut accessibles de l'extérieur. De ce fait, il prendra la même IP que votre machine hôte.

![Docker host network](https://devopssec.fr/images/articles/docker/networks/host_network_docker.png)

 3. Le réseau de type **MAC VLAN**
  L'utilisation du driver macvlan est parfois le meilleur choix lorsque vous utilisez des applications qui s'attendent à être directement connectées au réseau physique, car le driver Macvlan vous permet d'attribuer une adresse MAC à un conteneur, le faisant apparaître comme un périphérique physique sur votre réseau. Le moteur Docker route le trafic vers les conteneurs en fonction de leurs adresses MAC.
![Docker macvlan network](https://devopssec.fr/images/articles/docker/networks/macvlan_network_docker.jpg)
4. Le réseau de type **NONE**
	C'est le type de réseau idéal, si vous souhaitez interdire toute communication interne et externe avec votre conteneur, car votre conteneur sera dépourvu de toute interface réseau (sauf l'interface loopback).
	
5. Le réseau de type **OVERLAY**
Si vous souhaitez une mise en réseau multi-hôte native, vous devez utiliser un driver overlay. Il crée un réseau distribué entre plusieurs hôtes possédant le moteur Docker. Docker gère de manière transparente le routage de chaque paquet vers et depuis le bon hôte et le bon conteneur.
![Docker overlay network](https://devopssec.fr/images/articles/docker/networks/overlay_network_docker.png)

## Manipulation du réseau dans Docker

 1. Créer un réseau docker de type bridge
	 ```
	 docker network create --driver=bridge --subnet=192.168.2.0/24 sharenetwork
	 ```
	 ```
	 docker network ls
	 ```
	 
    |  NETWORK ID| NAME | DRIVER|SCOPE|
    |7c005a3c1bdf|bridge|  brige |local|
    | 2cdd7822b4d|   host |            host |     local |
    | f34d2829f7d3|   none |            null |     local |
    | 87a0482283f1|   sharenetwork |            bridge |     local |

 2. Créer deux conteneurs ubuntu dans le reseau crée précédement
 ```
 docker run -it --name ubuntu1 --network sharenetwork -d ubuntu /bin/bash
 docker run -it --name ubuntu2 --network sharenetwork -d ubuntu /bin/bash
 ```
 4. Installer la commande ping et tentez de pinguer les conteneurs entre eux avec leur ip et par leur nom
```
docker exec -it ubuntu1 /bin/bash
apt-get update && apt-get install iputils-ping
```
