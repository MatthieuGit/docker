
# Docker

## Introduction à la conteneurisation

 
Le terme d'***architecture monolithique*** désigne une application dont l'ensemble des modules(CMS, DAO, ESB) sont régroupés au sein d'une même entité. Une application monolithique est construire de manière à utiliser une base de données unique, une interface utilisateur, et une application côté serveur, et ne peut, par conséquent, qu’être exécuté dans son ensemble. Elle pourrait prendre le désigne suivant :

![image](https://user-images.githubusercontent.com/5073147/188262909-d4b1119c-d7db-4e75-b9e1-269b41723542.png)

Une telle architecture trouvent plusieurs limites :

 - La plupart du temps elle est écrite en utilisant un seul langage de
   programmation.
 - L'application est déployée sur la même machine
 - Lors de l'ajout d'un fix ou d'une évolution, cela nécessite de rendre
   indisponible l'ensemble de l'application pour effectuer la MAJ
 - Si on veut gérer la haute disponibilité, on doit acheter d'autres
   serveurs

Ainsi pour palier à ces problèmes, les architectures microservices se sont démocratisées. 
Une architecture microservices se caractérise par le fait de découper l'ensemble des modules en sous modules, les avantages d'une telle architecture est que l'ensemble des modules est indépendant des uns des autres et peuvent être installés sur des serveurs différents, ainsi les montées de versions sont plus flexible et ne nécessite plus un arrêt de service de l'ensemble de l'application mais seulement d'un module.
![image](https://user-images.githubusercontent.com/5073147/188264663-682ec7b3-cab3-453f-9148-40fcd8fb4bfe.png)

Une architecture microservices a les avantages suivants :

 - Les microservices favorisent l'organisation de petites équipes indépendantes, qui s'approprient leurs services. Les équipes agissent au sein d'un contexte de petite taille et bien compris, et peuvent travailler de manière plus indépendante et rapide améliorant l'agilité.
 - Flexibilité  car simplifie les processus de mise à jour des microservices, ainsi une meilleur performance
 - Scalabilité : permet aux équipes de dimensionner correctement les besoins de l'infrastructure, de mesurer de manière plus précise les coûts d'une fonctionnalité, et d'assurer la disponibilité lorsqu'un service enregistre un pic de demande
 - Résilience améliorée.L'indépendance du service augmente la résistance de l'application face aux défaillances. Dans une architecture monolithique, la défaillance d'un seul composant peut entraîner la défaillance de l'application toute entière. Avec l'architecture de microservices, les applications gèrent entièrement les échecs des services en dégradant la fonctionnalité, mais sans interrompre l'ensemble de l'application.

> Written with [StackEdit](https://stackedit.io/).
