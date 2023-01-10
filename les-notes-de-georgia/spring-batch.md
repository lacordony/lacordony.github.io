---
layout: default
category: notes
title: "Spring Batch"
---

# Spring Batch

J'ai travaillé sur Spring Batch durant une mission, je n'y connaissais rien et j'ai du comprendre et modifier du code que je n'avais jamais vu de ma vie. Dans tout ce que j'ai pu voir Spring Batch est ce que j'ai eu le plus de mal à comprendre. 

J'ai eu beau lire la [documentation officielle](https://docs.spring.io/spring-batch/docs/current/reference/html/index.html), ça me semblait hyper complexe et je n'arrivais pas à faire le lien entre l'application sur laquelle je travaillais et ce que je lisais.

Après cette mission, j'ai suivi une formation sur Udemy pour approfondir le sujet car je ne me sentais pas à l'aise du tout et j'ai compris beaucoup de choses à posteriori. La formation m'a vraiment aidée.

> "Même si l'expérience est sensée être la plus formatrice, un minimum de formation avant la mission m'aurait fait gagner beaucoup de temps !"

Dans cette note mon objectif sera de vous expliquer simplement ce qu'on ne m'avait pas expliqué et qui m'aurait vachement aidé.

## Concept

### Pourquoi Spring Batch ?

Spring Batch est très pratique par exemple lorsque vous devez migrer ou transformer des données d'un format A vers un format B. 

Il permet d'automatiser facilement l'ordonnancement de différentes tâches dépendantes les unes des autres, de les planifier pour qu'elles se déclenchent à certains intervalles de temps.

### Le fonctionnement de Spring Batch (jobs, tasklets etc...)

Spring Batch utilise des jobs qui vont lancer des étapes (steps ou tasklets) contenant des tâches.

Chaque step renverra un résultat FAIL, SUCCESS, STOPPED. Il est possible de paramétrer une étape pour qu'elle se relance en cas d'échec avant de passer à la suivante, que le job s'arrête si une step fail ou qu'il continue etc...



### La gestion des données

![Spring Batch Schema](/assets/img/spring-batch/springbatch-data.drawio.png)


## Job

## Tasklet

## Item Reader

## Item Writer

## Processor

## Exemples

J'ai gardé quelques échantillons exemples de la formation que j'ai pushé dans ce repository : 