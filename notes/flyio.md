---
layout: default
permalink: /notes/:basename
category: notes
title: "Déployer son application Spring Boot sur Fly.io"
status: published
last_updated: "01/04/2023"
---

Cette note a pour objectif d'expliquer comment déployer un dockerfile contenant une application Spring Boot sur [fly.io](https://fly.io/)

## Installer Fly sur Windows

Vous retrouverez toutes les infos en détails sur la [documentation officielle](https://fly.io/docs/hands-on/install-flyctl/)

Ouvrir Powershell et lancer la commande suivante :

```
iwr https://fly.io/install.ps1 -useb | iex
```

## S'authentifier en ligne de commande

Se connecter à votre compte via la commande suivante :

```
flyctl auth login
```

Personnellement j'ai créé mon compte via mon compte Github ce qui peut vous faciliter la tâche plus tard s'il peut accéder à vos repos.

## Déployer son application via Dockerfile

Pour pouvoir lancer notre application, il faut en pré-requis avoir un Dockerfile prêt à l'emploi.

Si vous ne savez pas comment générer votre Dockerfile je vous invite à revoir la note sur Docker.

Mais pas de panique, nous allons repartir de notre petit [projet Spring de demo](https://github.com/DevGeorgia/spring-with-docker-demo) qui contient déjà un Dockerfile.

Pour vous entraîner vous pouvez cloner ce repo.

Nous allons suivre ici la [documentation officielle de fly.io](https://fly.io/docs/languages-and-frameworks/dockerfile/)

On va donc se mettre à la racine de notre repo et ouvrir un terminal dans lequel nous allons exécuter la première commande :

```
fly launch
```

On va vous demander de renseigner certaines informations :
* Le nom de l'application : par exemple spring-with-docker-demo
* L'organisation
* La région : dans notre cas, cdg Paris, France
* Il va vous demander si vous voulez y ajouter des bases de données Postgresql ou Redis, vous pouvez dire non dans notre cas
* Il va vous demander si vous souhaitez déployer maintenant, vous pouvez dire oui dans notre cas car il n'y a pas de configuration supplémentaire à ajouter sur notre projet

La commande va pré-générer le fichier de configuration fly.toml pour vous qui servira à déployer l'application.

Vous pouvez rajouter dans le fichier de config des paramètres comme des variables d'environnements si vous avez des secrets à faire passer. Je ne vais pas rentrer dans les détails ici, vous pouvez regarder la documentation.

Ensuite, il va build votre image Docker et la pousser sur le registry Fly.

Si vous avez répondu "Non", à la question "voulez vous déployer maintenant ?", vous devrez lancer la commande suivante :
```
fly deploy
```

À la fin vous devrez voir apparaitre dans votre terminal le message : 
```
deployed successfully
```

Une fois le déploiement terminé, vous pouvez lancer la commande ci-dessous pour accéder à votre application : 
```
fly open
```

Et voir le résultat apparaître : *magic effect*

![fly-deploy](/assets/img/fly/flydeploySpringDemo.png)

Rendez-vous sur votre [dashboard fly.io](https://fly.io/dashboard) pour voir votre application tourner.

![fly-deploy](/assets/img/fly/flyDashboard.png)






