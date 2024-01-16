---
layout: default
permalink: /notes/:basename
title: "Développer une API REST avec Spring Boot"
category: notes
last_updated: "18/11/2023"
published: false
---

Spring est un Framework Java, tandis que Spring Boot est une extension de Spring qui permet de créer des applications autonomes, auto-configurées et prêtes à l'emploi.

## Qu'est-ce qu'une API REST ?

Quand on parle de Spring Boot, on parle souvent d'API REST. Mais qu'est-ce qu'une API ?

### Quelques définitions

#### API

Une API (Application Programming Interface) est un ensemble de fonctions qui permettent à des applications de communiquer entre elles.

Pour faire simple, on va mettre à disposition un service qui va permettre à d'autres applications de communiquer avec notre application.

#### REST

Et pourquoi REST alors ? REST signifie Representational State Transfer. C'est ce qu'on appelle un standard qui contient des normes ou règles d'architecture à suivre. Par exemple, il existe aussi SOAP (Simple Object Access Protocol) qui est un autre standard.

En Spring Boot, on est Restful. C'est-à-dire que l'on va utiliser les normes REST pour créer nos API.

Je ne vais pas entrer dans le détail sur les normes REST vous pouvez consulter ce cours d'OpenClassrooms si vous voulez en savoir plus : [Adoptez les API REST pour vos projets web](https://openclassrooms.com/fr/courses/6573181-adoptez-les-api-rest-pour-vos-projets-web)

### Les contrats

Ces API sont gérées par des contrats, c'est-à-dire que l'on va définir les règles de communication entre les applications.
* Qu'est-ce que j'attends en entrée ? 
* Qu'est-ce que je renvoie en sortie ? 
* Quels sont les codes d'erreur renvoyés ?

Ces API sont en général assorties d'une documentation permettant aux utilisateurs de comprendre comment les utiliser. Avec Spring Boot, vous entendrez souvent aussi parler de Swagger qui est un outil permettant de générer automatiquement une documentation à partir de vos API.

La communication va se faire via le protocole HTTP à l'aide de requêtes (GET, POST, PUT, DELETE etc...) et les données seront échangées au format JSON.

## Initialiser le projet

Pour initialiser votre projet simplement, vous pouvez vous rendre sur le site Spring Initializr : [https://start.spring.io/](https://start.spring.io/)

Vous pourrez choisir :
* Votre gestionnaire de dépendances : Maven / Gradle
* Votre language : Java / Kotlin / Groovy
* Votre version de Java
* Votre version de Spring Boot
* Le nom de votre projet et ses packages
* les dépendances dont vous avez besoin, par exemple pour une API REST, vous aurez besoin de Spring Web, Spring Data JPA, Spring Security etc...

![Spring initializr](/assets/img/spring/spring-initializr.png "img-code")

Une fois que vous avez tout sélectionné, vous pouvez cliquer sur Generate. Le site vous générera un fichier zip prêt à l'emploi que vous pourrez importer directement dans votre IDE.

Votre classe principale sera annotée @SpringBootApplication et contiendra la méthode main.

```
@SpringBootApplication
public class DemoApplication {

	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}

}
```

Cette annotation va permettre de configurer automatiquement votre application Spring Boot.

## Développer le CRUD de son application

### Le CRUD ?

Quand on développe des API, on parle aussi souvent de CRUD.

Le CRUD est un acronyme qui signifie Create, Read, Update, Delete. C'est un ensemble d'opérations de base que l'on peut effectuer sur une base de données et qui est sensé couvrir l'ensemble des use cases basiques d'une application.

Chaque lettre peut être associée à une requête HTTP :
* Create : POST
* Read : GET
* Update : PUT
* Delete : DELETE

Peu importe l'application que je développe ou les données que je manipule, j'aurais toujours besoin de pouvoir : créer une donnée, lire une donnée, mettre à jour une donnée ou supprimer une donnée.

### Le contrôleur REST

Pour créer une API REST, il faut commencer par créer un contrôleur REST.

Un contrôleur REST est une classe Java qui va contenir les méthodes permettant de créer, lire, mettre à jour ou supprimer des données.

Pour créer un contrôleur REST, il faut ajouter l'annotation @RestController sur la classe.

```
@RestController
public class MyController {
}
```


### Les DTO (Data Transfer Object)

Les DTO sont des classes qui vont permettre de transférer des données entre les couches de votre application.



### Les requêtes HTTP

#### GET

#### POST

#### PUT

#### DELETE

### En synthèse

| CRUD   | HTTP   | API Endpoint (URI) | Annotation     |
|--------|--------|--------------------|----------------|
| Create | POST   | /api/item          | @PostMapping   |
| Read   | GET    | /api/item/{id}     | @GetMapping    |
| Read   | GET    | /api/items         | @GetMapping    |
| Update | PUT    | /api/item/{id}     | @PutMapping    |
| Delete | DELETE | /api/item/{id}     | @DeleteMapping |





## Documenter l'API avec Swagger


## Pour aller plus loin

Je vous recommande la [Spring Academy](https://spring.academy/) qui a été créée assez récemment et qui contient des formations complètes avec une possible certification à la clé.

Côté référents vous avez le site de [Baeldung](https://www.baeldung.com/) qui regorge d'exemples.

Niveau formation vous avez également un cours OpenClassrooms : [Créez une application Java avec Spring Boot](https://openclassrooms.com/fr/courses/6900101-creez-une-application-java-avec-spring-boot)
