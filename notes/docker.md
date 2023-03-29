---
layout: default
category: notes
title: "Docker"
status: brouillon
last_updated: "28/03/2023"
---


En entreprise on voit que de plus en plus de choses sont automatisées avec des chaînes devops, notamment les chaînes de déploiement. 

> "En tant que développeur junior on ne voit pas toujours ce qui se passe après le développement. Mon code est pushé, il a été mergé et après ?"

J'ai commencé à m'intéresser à la question quand j'ai voulu déployer un site web perso. Par exemple, cette Github Pages est configurée pour se déployer automatiquement à chaque push du coup je n'ai pas trop à me soucier de ce qu'il se passe. Juste un clic pour choisir la branche à déployer et c'est fait, le pipeline se lance tout seul et le site est en ligne.

Mais pour un site web homemade ? 

J'ai commencé à développer un site en Spring/Thymeleaf car Spring est ma stack pro et je voulais un site pour m'entrainer, bidouiller, explorer. Je voyais tout le monde parler de Netlify et de sa facilité de déploiement, je pensais que ça me prendrait que quelques minutes. Sauf que voilà, Netlify ne gère que le déploiement de sites statiques. Pour le java vous repasserez.

Du coup, pour déployer mon site, je dois générer une image Docker et la déployer. L'angoisse totale.

> "Je n'ai jamais appris Docker, ni en formation ni dans mon expérience pro, alors que ça semble être un incontournable."

L'objectif de cette note sera donc de :
* Installer Docker sur Windows
* Comprendre ce que c'est et comment ça marche
* Créer un dockerfile à partir d'un projet Spring Boot / Maven et le pousser sur le docker hub

Pour ce qui est de l'automatisation et du déploiement, on verra ça plus tard à travers une autre note qui parlera de fly.io

Pour écrire cette note j'ai utilisé les sources suivantes : le site officiel pour l'installation de [Docker](https://docs.docker.com/get-docker/), le cours openclassrooms [Optimisez vos déploiements en créant des conteneurs avec Docker](https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker) et la playlist youtube des [vidéos](https://www.youtube.com/watch?v=3hol91BkYHU&list=PLmw3X80dPdlyRV2EUKnFOvBACs_tcArd0) de [@aurelievache](https://twitter.com/aurelievache) 

## Installation

Rendez-vous sur le site de Docker pour télécharger et installer [Docker Desktop](https://docs.docker.com/get-docker/)

Je vous fais pas un dessin, c'est très bien expliqué, j'ai suivi pas à pas l'installation et rien n'a explosé !

Si vous êtes sur Windows comme moi (oui ça existe), veillez à bien avoir WSL 2 d'installé avant pour avoir une distribution linux compatible, vous retrouverez les instructions [ici](https://learn.microsoft.com/en-us/windows/wsl/install).

## Docker, c'est quoi ? 

Sur les projets sur lesquels je travaille, on utilise des VM (machine virtuelle) sur lesquelles nos programmes sont exécutés. Sur ces machins on retrouve en général un OS Linux/Windows, ça ressemble à votre PC perso mais vous y accédez à distance. Alors c'est cool on peut faire plein de trucs avec, mais ça consomme aussi beaucoup de ressources (CPU/RAM) et potentiellement d'argent. Ces VMs ont une certaine capacité que vous devez définir à l'avance, vous devez aussi savoir de combien de machines vous aurez besoin. Il faut donc anticiper et souvent, quand on sait pas trop anticiper, on a tendance à prendre de la marge. Du coup on achète plein de grosses machines et in fine on en utilise que 20%. Pas super opti ! Ni pour le portefeuille, ni pour la planète.

Bref.

C'est pour ces raisons notamment que la conteneurisation d'applications est devenue à la mode. Je vais reprendre la symbolique du bateau et des containers mais en gros au lieu d'avoir 3 bâteaux pour déplacer vos 3 cargaisons, vous allez mettre vos cargaisons dans 3 containers qui vont être déposées sur le même bateau. Les containers peuvent donc être de tailles différentes et être gérés indépendamment par le bateau.

Techniquement parlant on va packager notre application dans un conteneur ce qui va faciliter l'automatisation des déploiements et aussi leur rapidité. De plus, les conteneurs ne consommeront que les ressources nécessaires à leur fonctionnement, moins de gaspillage de ressources et d'argent. Enfin, on n'est plus dépendant de l'OS, le conteneur pourra être déployé partout.

## Lancer un conteneur



## Créer son premier docker file 


## Orchestrer ses conteneurs avec Docker Compose


## En synthèse : les commandes


### Container





### Image

L'image contient tout ce qui est nécessaire au lancement d'une application.
Une image est représentée par un id (imageID) et un nom (repository). Le nom pointe vers un imageID. Plusieurs noms peuvent pointer vers une même image.
Chaque image contient plusieurs couches (layers).

* Afficher la liste des images disponibles
```
docker images
```

* Filtrer la liste des images
```
docker images --filter reference="commencepar*:*finipar"
```

* Lister les images non utilisées
```
docker images -f dangling=true
```

* Supprimer une image
```
docker images rmi ubuntu:latest
```

### Layers

Les layers font partie d'une image. Les layers sont identifiés par un id.
Les layers sont en lecture seule et ne peuvent être modifiés.
