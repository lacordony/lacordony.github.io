---
layout: default
category: notes
title: "Débuter avec Docker"
status: published
last_updated: "02/04/2023"
---


En entreprise on voit que de plus en plus de choses sont automatisées avec des chaînes devops, notamment les chaînes de déploiement. 

> "En tant que développeur junior on ne voit pas toujours ce qui se passe après le développement. Mon code est pushé, il a été mergé et après où est-ce qu'il va ?"

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

Sur les projets sur lesquels je travaille, on utilise des VM (machine virtuelle) sur lesquelles nos programmes sont exécutés. Sur ces machines on retrouve en général un OS Linux/Windows, ça ressemble à votre PC perso mais vous y accédez à distance. Alors c'est cool on peut faire plein de trucs dessus, mais ça consomme aussi beaucoup de ressources (CPU/RAM) et potentiellement beaucoup d'argent. Ces VMs ont une certaine capacité que vous devez définir à l'avance, vous devez aussi savoir de combien de machines vous aurez besoin. Il faut donc anticiper et souvent, quand on ne sait pas trop anticiper, on a tendance à prendre de la marge. Du coup on achète plein de grosses machines et in fine on en utilise que 20%. Pas super opti ! Ni pour le portefeuille, ni pour la planète.

Bref. C'est pour ces raisons notamment que la conteneurisation d'applications est devenue à la mode. Je vais reprendre la symbolique du bateau et des containers mais en gros au lieu d'avoir 3 bâteaux pour déplacer vos 3 cargaisons, vous allez mettre vos cargaisons dans 3 containers qui vont être déposés sur le même bateau. Les containers peuvent donc être de tailles différentes et être gérés indépendamment par le bateau.

Techniquement parlant on va packager notre application dans un conteneur ce qui va faciliter l'automatisation des déploiements et aussi leur rapidité. De plus, les conteneurs ne consommeront que les ressources nécessaires à leur fonctionnement, moins de gaspillage de ressources et d'argent. Enfin, on n'est plus dépendant de l'OS, le conteneur pourra être déployé partout.

Si vous préférez quelque chose d'un peu plus visuel, vous pouvez regarder le [schéma d'architecture](https://docs.docker.com/get-started/overview/#docker-architecture) officiel de Docker.

## Lancer un conteneur

Pour lancer votre conteneur, il vous faut une image. Il existe des images sur le Docker Hub (aussi appelé Registry) c'est un peu comme aller chercher ses packages sur NPM finalement.

On va donc aller chercher l'image ["hello-world"](https://hub.docker.com/_/hello-world) et lancer un conteneur via la commande :

```
docker run hello-world
```

La commande va chercher si l'image existe en local sinon elle va aller la pull sur le Docker Hub.

![docker-run](/assets/img/docker/helloworldocker.png)

Pour ceux qui utilisent Docker Desktop vous allez le voir apparaitre dans votre liste de container.

![docker-run](/assets/img/docker/containerhelloworld.png)

Avec un "docker run" standard votre conteneur ne va pas rester allumé.

Pour ça il faut le lancer dans une console indépendante via l'argument "-d" (pour detach)

```
docker run -d -p 80:80 docker/getting-started
ou
docker run -dp 80:80 docker/getting-started
```

L'argument "-p" permet de définir le port, ici 80:80. 
Une fois votre conteneur lancé vous pourrez vous rendre à l'adresse suivante : http://localhost:80/ et vous retrouverez la documentation de démarrage.

Vous voyez dans le docker desktop que cette fois le conteneur n'est pas arrêté.

![docker-run](/assets/img/docker/containergettingstarted.png)

Si vous n'en avez plus besoin vous pouvez l'arrêter.

```
docker stop <ID_DU_CONTAINER>
```

Une précision importante. Lorsque vous stoppez votre conteneur toute donnée sera perdue, c'est ce qu'on appelle un conteneur stateless (sans état). C'est à dire qu'il n'y a aucune persistance de données dans le conteneur.
Si vous voulez héberger par exemple une base de données, vous devrez utiliser un conteneur stateful (avec état) qui ne supprimera pas les données à l'arrêt du conteneur.

## Créer son premier dockerfile 

Pour cette partie, je vais partir d'un projet basique [Spring Boot - Hello World](https://github.com/GeorgiaLR/spring-with-docker-demo) que j'ai créé pour le test. On va se baser sur le Dockerfile d'exemple sur la [doc Spring](https://spring.io/guides/topicals/spring-boot-docker/).

Vous pouvez cloner le projet pour tester, j'ai déjà créé un fichier Dockerfile à la racine :
```
FROM eclipse-temurin:17-jdk-alpine
VOLUME /tmp
COPY target/*.jar spring-with-docker-0.0.1-SNAPSHOT.jar
ENTRYPOINT ["java","-jar","/spring-with-docker-0.0.1-SNAPSHOT.jar"]
```

Pour récapituler on a besoin de FROM pour définir notre jdk, VOLUME pour définir où vont être stockées les ressources de notre conteneur, COPY pour lui dire de copier le jar généré dans notre dossier target. Et enfin ENTRYPOINT qui va contenir la commande que l'on veut lancer à savoir notre java -jar etc...

Vous retrouverez un petit tableau synthèse des différents arguments en bas de cette note.

NB : Pour un projet javascript par exemple, le dockerfile sera légèrement différent vous utiliserez notamment l'argument RUN. Ce n'est pas la cible de cette note, vous trouverez un [exemple sur la documentation officielle](https://docs.docker.com/get-started/02_our_app/).


Pour build l'image correspondante exécutez la commande ci-dessous dans votre terminal :
```
docker build -t spring-with-docker-demo .
```

Votre image apparaitra sur votre docker desktop :
![docker-build-spring](/assets/img/docker/imageSpringDemo.png)

Pour lancer votre conteneur, exécutez ensuite la commande ci-dessous dans votre terminal : 
```
docker run -dp 8080:8080 spring-with-docker-demo
```

Votre conteneur est lancé :
![docker-run-spring](/assets/img/docker/containerSpringDemo.png)

Rendez-vous ensuite à l'adresse localhost:8080 et vous devriez voir le résultat apparaître :

![docker-localhost-spring](/assets/img/docker/ResultSpringHelloWorld.png)

Cool, cool, cool !

Pour finir, vous voulez sans doute pouvoir partager votre image sur le registry [Docker Hub](https://hub.docker.com/)

On va d'abord relier notre image à notre registry via un tag (remplacez HUB_USERNAME par votre pseudo Docker Hub)
```
docker tag spring-with-docker-demo:latest HUB_USERNAME/spring-with-docker-demo:latest
```

Ensuite on va pusher notre image (remplacez HUB_USERNAME par votre pseudo Docker Hub)
```
docker push HUB_USERNAME/spring-with-docker-demo:latest
```

Le mot "latest" signifie la version la plus récente et celle qui sera prise par défaut. Vous pouvez tout à faire versionner vos images "spring-with-docker-demo:1.0.0" par exemple, mais ce sera toujours latest qui sera téléchargée par défaut.

Vous pouvez vous connecter ensuite sur le docker hub et voir votre image :
![docker-hub-spring](/assets/img/docker/dockerHubResultPush.png)

À noter qu'il existe d'autres registry comme le [Github Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry) qui vous permet de stocker vos images liées à vos repos Github par exemple. On en reparlera sans doute dans une note pour automatiser le déploiement des images avec des Github Actions.

## Orchestrer ses conteneurs avec Docker Compose

Lancer un conteneur c'est bien, mais dans la réalité vous aurez probablement rarement un seul conteneur à lancer pour faire tourner votre application.

Cas typique numéro 1, votre base de données doit être dans un conteneur stateful donc il est probable que vous vouliez l'isoler du reste. Autre cas possible vous avez une application front et une application back qui sont packagées dans deux projets différents. Ou encore vous avez une architecture micro-services avec plein de services que vous voulez séparer mais qui ont besoin les uns des autres.

Pour être certain que l'on retrouve tous nos petits, on voudrait s'assurer que notre déploiement n'oublie personne. Ce serait dommage de ne déployer que la moitié de l'application.

Pour ça on peut utiliser Docker-compose qui est un orchestrateur de conteneurs.

Cette fois, on ne va plus utiliser un Dockerfile mais un fichier yaml : docker-compose.yml.

Partant de notre projet Spring de Demo, imaginons que l'on ait besoin de se connecter à une base de données MySQL pour enregistrer ou lire des informations.

Pour cela, nous allons créer un fichier docker-compose.yml pour orchestrer nos deux conteneurs.

Ce qu'il faut retenir c'est que ce fichier contient votre stack, et que cette stack est composée d'un ensemble de services (les différents conteneurs).

Rendez-vous sur la branche "docker-compose" du [repo de Demo]() pour utiliser le fichier déjà prêt (remplacez HUB_USERNAME si vous avez push l'image sinon vous pouvez utiliser mon pseudo georgialr)

```
version: '3.1'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: powerpass
      MYSQL_DATABASE: demo
      MYSQL_USER: springuser
      MYSQL_PASSWORD: springpass

  spring-demo:
    depends_on:
      - db
    image: HUB_USERNAME/spring-with-docker-demo:latest
    ports:
      - "8000:80"
    restart: always

volumes:
  db_data: {}
```

Qu'est-ce que nous raconte ce fichier ?

Tout d'abord on lui indique la version de Docker-compose que l'on veut utiliser. Ensuite on va lui lister nos services, dans notre cas nous avons 2 services notre db Mysql et notre application Spring de demo. Chaque service va contenir ses propres paramètres notamment le nom de l'image associée. Vous pouvez vous rendrez sur le docker hub de l'image pour avoir un exemple détaillé de tous les paramètres attendus de votre image. Pour le cas de MySQL on va lui attribuer un volume qui permettra d'assurer la persistance de données pour qu'elles ne soient pas perdues au redémarrage du service.

Pour build votre package exécutez la commande suivante :
```
docker-compose pull
```

Enfin pour lancer vos conteneurs lancez la commande : 
```
docker-compose up -d
```

Vos conteneurs sont lancés :

![docker-compose-result](/assets/img/docker/dockerComposeSpringDemo.png)


## En synthèse : les commandes

### Container

* Lancer un conteneur
```
docker run <IMAGE>
```

* Lancer un conteneur détaché avec un port défini
```
docker run -dp <PORT> <IMAGE>
```

* Arrêter un conteneur
```
docker stop <ID_DU_CONTAINER>
```

* Download une image du registry en local
```
docker pull <IMAGE>
```

* Supprimer un conteneur
```
docker rm <ID_DU_CONTAINER>
```

* Afficher la liste des conteneurs détachés
```
docker ps
```

### Image

L'image contient tout ce qui est nécessaire au lancement d'une application.
Une image est représentée par un id (imageID) et un nom (repository). Le nom pointe vers un imageID. Plusieurs noms peuvent pointer vers une même image.
Chaque image contient plusieurs couches (layers).

* Afficher la liste des images disponibles
```
docker images
```

* Afficher la liste des images disponibles en local
```
docker images -a
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


### Dockerfile

| Commande   | Description                                     |
|------------|-------------------------------------------------|
| FROM       | Définit l'image de base (OS/JDK)                |
| MAINTAINER | Nom de l'auteur/gestionnaire                    |
| COPY       | Copie les fichiers vers une destination         |
| ADD        | Ajoute des fichiers                             |
| RUN        | Lance une commande                              |
| WORKDIR    | Définit un répertoire de travail par défaut     |
| CMD        | Définit une commande par défaut                 |
| ENTRYPOINT | Définit une commande et ses paramètres          |
| ENV        | Permet de définir des variables d'environnement |
| EXPOSE     | Permet de définir un port par défaut            |

Vous pouvez retrouver une description détaillée sur [cette cheatsheet](https://kapeli.com/cheat_sheets/Dockerfile.docset/Contents/Resources/Documents/index)

### Docker-compose

* Vérifier la validité de votre fichier docker-compose.yml
```
docker-compose config
```

* Télécharger les images de votre stack
```
docker-compose pull
```

* Lancer les conteneurs de votre stack
```
docker-compose up -d
```

* Vérifier le statut de votre stack
```
docker-compose ps
```

* Vérifier les logs de votre stack
```
docker-compose logs -f --tail 5
```

* Stopper les conteneurs de votre stack
```
docker-compose stop
```

* Supprimer le contenu de la stack 
```
docker-compose down
```

Récapitulatif des arguments du fichier docker-compose.yml :

| Commande    | Description                                          |
|-------------|------------------------------------------------------|
| version     | La version de docker compose utilisée                |
| image       | le nom de l'image à télécharger                      |
| volumes     | le chemin vers le volume persistant le cas échéant   |
| restart     | le comportement en cas d'erreur, doit il se relancer |
| environment | les variables d'environnement à ajouter (key/value)  |
| depends_on  | si un conteneur dépend d'un autre pour se lancer     |
| ports       | les ports du service le cas échéant                  |

