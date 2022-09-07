Module-3_TP2: Gestion des images

 1. Image docker
 Une image docker est constitué de plusieurs couches (layer):
 
	 1. Base de l'image (centos, ubuntu, alpine)
	 2. librairies de l'os
	 3. les dépendances
	 4. l'application
	 
Le dockerfile permet de décrire l'ensemble des étapes à suivre pour construire un contener contenant notre service. L'image est le réceptacle de l'ensemble des étapes décrit dans le dockerfile.

2.	Contenu d'un dockerfile
FROM : Spécifie la base de l'image
MAINTENER: Spécifie le mainteneur de l'image (son nom par exemple)
RUN: Execute une commande
ADD: Ajoute un fichier ou un répertoire
EXPOSE: les ports d'accès à l'application
ENV: Créé une variable d'environnement

Différence entre ENTRYPOINT et CMD:
Les deux commandes sont utilisées pour spécifier les commandes a executer lors de l'initialisation du conteneur à partir de l'image

CMD : Définie les paramètres par défaut pouvant être remplacé à partir de la commande de lancement d'un conteneur
ENTRYPOINT: Paramètre par défaut ne pouvant pas être remplacé lors de l'execution d'un conteneur en ligne de commande.

Différence entre COPY et ADD:
COPY et ADD sont deux instructions Dockerfile qui ont des objectifs similaires. Ils permettent de copier des fichiers d'un emplacement spécifique dans une image Docker.

COPY prend une source et une destination. Il permet uniquement de copier un fichier ou un répertoire local de votre hôte (la machine créant l'image Docker) dans l'image Docker elle-même.

ADD permet de le faire aussi, mais il prend également en charge 2 autres sources:

 1. Il peut utiliser une URL au lieu d'un fichier/répertoire local
 2. Il peut extraire un fichier tar de la source directement dans la destination.

3. Contenu d'une image permettant de créér un serveur  web

> FROM ubuntu
MAINTAINER mattGithub (matth.bailly@gmail.com)
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y nginx git
EXPOSE 80
#ADD static-website-example/ /var/www/html/
RUN rm -rf /var/www/html/*
RUN git clone https://github.com/diranetafen/static-website-example.git /var/www/html/
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

4. Compilation d'une image docker
```
docker build -t webapp:v1 .
-t pour tag
```
5. Vérification de la présence de l'image 
```
docker images
```
6. Execution d'un conteneur à partir de l'image
```
docker run --name webapp -d -p 80:80 webapp:v1
```

