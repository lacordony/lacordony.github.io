---
layout: default
permalink: /notes/:basename
category: notes
title: "Maîtriser la qualité du code avec Sonarqube"
published: false
last_updated: "02/04/2023"
---

Récemment Github a fait [un sondage](https://twitter.com/github/status/1643724794192609280) pour savoir combien le mentorat avait été important pour les techs dans leur carrière. J'avoue avoir été suprise du résultat : 47% ont répondu n'avoir jamais été mentorés. Ce qui est mon cas aussi, mais je pensais faire partie des exceptions pas de la règle.

Ne pas être mentoré c'est assez compliqué quand on débute car on a pas de feedbacks sur notre performance. On ne sait pas ce qu'on fait bien ou mal, ni comment s'améliorer. Alors comment on s'assure de la qualité de notre code ?

Sonarqube est un bon outil pour vous y aider.

"SonarQube est un logiciel libre de qualimétrie en continu de code. Il aide à la détection, la classification et la résolution de défaut dans le code source, permet d'identifier les duplications de code, de mesurer le niveau de documentation et connaître la couverture de test déployée." Source : [Wikipédia](https://fr.wikipedia.org/wiki/SonarQube)

## Quelles métriques de qualité puis-je contrôler ?

SonarQube ne mesure pas tout mais peut vous aider à identifier un certain nombre de problèmes.
* Le taux de couverture de tests
* Le nombre de duplications de code
* La complexité du code : si vous avez trop de boucles for et if dans une même méthode, votre complexité va fortement augmenter et Sonar vous demandera de splitter votre méthode
* Les bugs potentiels : Sonar définit comme "Bug" des éléments de code qui peuvent conduire à un bug. Votre code va fonctionner en l'état mais il n'est pas assez "safe". 
* Le code smell : Sonar définit comme "code smell" des éléments de code qui correspondent à de mauvaises pratiques
* La dette technique

Toutes ces métriques vous aideront à limiter la casse.

## Installation de Sonarqube avec Docker

On va utiliser Docker pour se faciliter la vie, si vous ne connaissez pas Docker je vous renvoie vers cette [note]().

```
docker pull sonarqube
```


```
docker run --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest
```

Si vous voulez d'autres alternatives d'installation, c'est par [ici](https://docs.sonarqube.org/latest/setup-and-upgrade/install-the-server/)


## Configuration de Sonarqube

### Configuration avec Maven

Agent Sonar / Serveur Sonar

Quality gate : ensemble de seuils à ne pas dépasser

Quality profile :

### Configuration avec Gradle

Prochainement.

## Jacoco pour les tests unitaires



## Complément : Configurer le Plugin Sonarlint


https://plugins.jetbrains.com/plugin/7973-sonarlint