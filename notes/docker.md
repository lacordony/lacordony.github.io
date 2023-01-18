---
layout: default
title: "Docker"
---


En entreprise on voit que de plus en plus de choses sont automatisées avec des chaînes devops, notamment les chaînes de déploiement. 

> "En tant que développeur junior on ne voit pas toujours ce qui se passe après le développement. Mon code est pushé, il a été mergé et après ?"

J'ai commencé à m'intéresser à la question quand j'ai voulu déployer un site web perso. Par exemple, cette Github Pages est configurée pour se déployer automatiquement à chaque push du coup je n'ai pas trop à me soucier de ce qu'il se passe. Juste un clic pour choisir la branche à déployer et c'est fait, le pipeline se lance tout seul et le site est en ligne.

Mais pour un site web homemade ? 

J'ai commencé à développer un site en Spring/Thymeleaf car Spring est ma stack pro et je voulais un site pour m'entrainer, bidouiller, explorer. Je voyais tout le monde parler de Netlify et de sa facilité de déploiement, je pensais que ça me prendrait que quelques minutes. Sauf que voilà, Netlify en fait ne gère que le déploiement de site statique donc pour le java vous repasserez.

Du coup, pour déployer mon site, je dois générer une image Docker et la déployer. L'angoisse totale.

> "Je n'ai jamais appris Docker, ni en formation ni dans mon expérience pro, alors que ça semble être un incontournable."

L'objectif de cette note sera donc de :
* Installer Docker sur Windows
* Comprendre ce que c'est et comment ça marche (Source : https://www.youtube.com/watch?v=3hol91BkYHU&list=PLmw3X80dPdlyRV2EUKnFOvBACs_tcArd0)
* Build une image en local à partir d'un projet Springboot / Maven

Pour aller plus loin et la déployer, on ira voir comment marche fly.io, mais ça, ce sera pour une autre note.

## Installation sur Windows

Rendez-vous sur le site de Docker pour télécharger et installer Docker Desktop
https://docs.docker.com/desktop/install/windows-install/



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

