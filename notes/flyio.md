---
layout: default
title: "Docker"
status: brouillon
---

# Déployer son application Spring Boot sur Fly.io

Cette note a pour objectif d'expliquer comment déployer son dockerfile sur fly.io

## Installer Fly sur Windows

Vous retrouverez toutes les infos en détails sur la [documentation officielle](https://fly.io/docs/hands-on/install-flyctl/)

Ouvrir Powershell et lancer la commande suivante :

``iwr https://fly.io/install.ps1 -useb | iex``

Se connecter à votre compte via la commande suivante :

``flyctl auth login``

Personnellement j'ai créé mon compte via mon compte Github


## 

Si vous ne savez pas comment générer votre docker file je vous invite à revoir la note sur Docker.

