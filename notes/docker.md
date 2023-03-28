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

## Installation sur Windows

Rendez-vous sur le site de Docker pour télécharger et installer [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/)




## Image


Réprésentées par un id (imageID) et un nom (repository)
Le nom pointe vers un imageID
Plusieurs noms peuvent pointer vers une même image.
Chaque image contient plusieurs couches (layers)
L'image contient tout ce qui est nécessaire au lancement d'une application.

Afficher la liste des images disponibles
docker images

Filtrer la liste des images
docker images --filter reference="commencepar*:*finipar"

Lister les images non utilisées
docker images -f dangling=true

Supprimer image
docker images rmi ubuntu:latest

## Layers

Les layers font partie d'une image
Layers sont en lecture seule, ne peuvent être modifiés
Layers identifiés par un id



## Container

