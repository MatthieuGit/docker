Module-2_TP1: installation docker

 1. Installation de Docker
https://docs.docker.com/engine/install/ubuntu/#install-from-a-package
	 1. Soit par le dépot Docker
	 2. Soit par une installation manuelle
	 3. Soit par le script
2 - Tâche de post installation
Dans le but de pouvoir utiliser docker sans les priviléges root, on peut ajouter notre utilisateur au groupe Docker
pour cela il faut ajouter un group docker
```
sudo groupadd docker
```
Puis ajouter notre utilisateur courant au groupe
```
 sudo usermod -aG docker $USER
```
3 - Vérification de l'installation
```
 docker --version
 docker run hello-world
```
4 - Utilisation de la documentation Docker

```
man docker
```
sur google 
docker docs
docker run arguments

5 - Lancement de votre 1er conteneur nginx
```
docker container run -d --name nginx -p 80:80 nginx
```
```
docker container ls
```
6 - Utilisation des variables d'environnements


