---
layout: NoteLayout
permalink: /notes/:basename
category: notes
title: "Spring Batch"
last_updated: "01/05/2023"
published: false
status: brouillon
---

J'ai travaillé sur Spring Batch durant une mission, je n'y connaissais rien et j'ai dû comprendre et modifier du code que je n'avais jamais vu de ma vie. Dans tout ce que j'ai pu voir Spring Batch est ce que j'ai eu le plus de mal à comprendre. 

J'ai eu beau lire la [documentation officielle](https://docs.spring.io/spring-batch/docs/current/reference/html/index.html), ça me semblait hyper complexe et je n'arrivais pas à faire le lien entre l'application sur laquelle je travaillais et ce que je lisais.

Après cette mission, j'ai suivi une formation sur Udemy pour approfondir le sujet, car je ne me sentais pas à l'aise du tout et j'ai compris beaucoup de choses à posteriori. La formation m'a vraiment aidée.

> "Même si l'expérience est censée être la plus formatrice, un minimum de formation avant la mission m'aurait fait gagner beaucoup de temps !"

Dans cette note mon objectif sera de vous expliquer simplement ce qu'on ne m'avait pas expliqué et qui m'aurait vachement aidé.

## Concept

### Pourquoi Spring Batch ?

Spring Batch est très pratique par exemple lorsque vous devez migrer ou transformer des données d'un format A vers un format B. 

Il permet d'automatiser facilement l'ordonnancement de différentes tâches dépendantes les unes des autres, de les planifier pour qu'elles se déclenchent à certains intervalles de temps.

### Le fonctionnement de Spring Batch

Spring Batch utilise des jobs qui vont lancer des étapes (steps ou tasklets) contenant des tâches.

![Spring Batch Schema](/assets/img/spring-batch/springbatch.drawio.png)

Chaque step renverra un résultat FAIL, SUCCESS, STOPPED etc... Il est également possible de paramétrer une étape pour qu'elle se relance en cas d'échec avant de passer à la suivante, mais aussi que le job s'arrête si une step fail ou qu'il continue etc...

En bref, vous avez une multitude de façons d'ordonnancer vos traitements.

## Et en pratique ?

Notez déjà que vous pourrez voir deux façons d'utiliser Spring Batch : avec un fichier de configuration XML ou avec une configuration annotée et codée (depuis Spring 3).

Personnellement les projets sur lesquels j'ai travaillé utilisaient un fichier de configuration XML (ou plusieurs) et j'ai eu beaucoup de mal à les déchiffrer. Sachant que déjà je ne comprenais pas beaucoup le fonctionnement de Spring Batch, mais alors pour déchiffrer le lien entre le contenu du XML et ce qui se passe dans le code, beaucoup de nœuds au cerveau.

> "La configuration XML c'est beaucoup de nœuds au cerveau."

Après je comprends le choix de passer par un XML, c'était plus facile à modifier à la volée pour faire des tests ou des modifications qui ne nécessitaient pas de tout rebuild et redéployer.  Si vos chaînes de déploiement sont lourdes et complexes, vous préférerez peut-être passer par un fichier de config XML.

Vous ne verrez pas de configuration XML dans mes repos Git, mais j'essaierais si j'ai le temps et que c'est possible de vous montrer les deux façons de faire dans cette note.

Je ne vais pas vous faire une demo de [Spring Initializr](https://start.spring.io/) ici, vous pouvez jeter un oeil aux dépendances qui peuvent être nécessaires dans ce [Pom.xml](https://github.com/DevGeorgia/spring-batch-demo/pom.xml)

### Avant-propos : versions de Spring

Lorsque j'ai suivi ma formation, nous étions en Spring version 2.7.1, j'ai constaté que certaines API étaient devenues deprecated depuis (JobBuilderFactory, StepBuilderFactory).

J'ai donc créé un repo git pour refaire un exemple adapté en Spring version 3.0.6. Ce n'est pas une mince affaire quand les choses changent de migrer vers une nouvelle version.

### Job

Commençons par le commencement, on a besoin d'un job.

#### Annotations et configuration

Précision : En Spring Boot 2 vous avez pu voir cette annotation @EnableBatchProcessing qui était indispensable au lancement de vos jobs. En Spring Boot 3, le comportement de l'annotation a changé. Si vous l'activez vos batchs ne se lanceront pas automatiquement au démarrage c'est un peu devenu l'équivalent de la property : spring.batch.job.enabled=false
Donc si vous voulez que votre code s'exécute au lancement ne l'ajoutez pas. J'ai perdu un temps fou à chercher pourquoi mes jobs ne fonctionnaient plus, j'ai eu du mal à trouver cette info pourtant centrale.

La classe contenant votre job doit être annotée par @Configuration

```
@Configuration
public class MyJob {

}
```

#### Datasource

Important à savoir et à comprendre, un job a besoin d'une base de données pour stocker les informations relatives au job (son status, ses paramètres etc..)

Il faut donc lui fournir une datasource pour que le job repository puisse aller sauvegarder les informations dans la base de données.

Par défaut si vous ne lui donnez rien, il va créer une base In Memory H2. Utile pour vos tests mais déconseillé pour une vraie application car si vous éteignez votre serveur vous perdez tout.

* Application.properties

Voici un exemple de properties pour une base Mysql :

```
spring.datasource.url=jdbc:mysql://<URL>:<PORT>/<DB_NAME>
spring.datasource.username=<USERNAME>
spring.datasource.password=<PASSWORD>
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

#Crée le schéma et les tables au démarrage
spring.batch.initialize-schema=always
```

Alors ça c'est bien, mais en réalité, est ce que vous avez envie de mélanger votre DB qui va gérer vos jobs et la DB qui va gérer vos vraies données ? (Celles que vous allez migrer)

Vous pouvez tout à fait avoir 2 datasources distincts.

```
spring.batchdatasource.url=jdbc:mysql://<URL>:<PORT>/<DB_NAME>
spring.batchdatasource.username=<USERNAME>
spring.batchdatasource.password=<PASSWORD>
spring.batchdatasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.realdatasource.url=jdbc:mysql://<URL>:<PORT>/<DB_NAME>
spring.realdatasource.username=<USERNAME>
spring.realdatasource.password=<PASSWORD>
spring.realdatasource.driver-class-name=com.mysql.cj.jdbc.Driver

#Crée le schéma et les tables au démarrage
spring.batch.initialize-schema=always
```

* Classe Datasource





#### Job launcher



#### Job Parameters

#### Job Status


### Step : Tasklet




### Step : Chunk-oriented


![Spring Batch Chunk Schema](/assets/img/spring-batch/springbatch-chunk.drawio.png)

Pour vous expliquer plus simplement cette partie je vais illustrer avec un exemple.

Admettons que vous ayez une plateforme de suivi des examens/évaluations de vos étudiants. On vous annonce que demain vous allez devoir changer de plateforme pour un truc mieux. Sauf que, vous voulez pouvoir garder les évaluations de l'année scolaire en cours pour ne pas avoir à switcher entre les deux. On vous propose alors de migrer ces données vers la nouvelle plateforme.

Pour cela, on va vous mettre à dispo un programme qui va aller récupérer les données au format A dans une source A (répertoire, base de données) pour les migrer dans un format B vers une destination B (répertoire, base de données).

Pour notre exemple, je vais partir du principe que le format A sera un CSV et le format B sera un JSON.

Voici un exemple de ce que contiendra le CSV d'input :

```
ID;First Name;Last Name;area;exam;score
1;John;Smith;Geography;Oceans;8
2;Pierre;Dupont;History;World war One;4
3;Paul;Durant;Maths;Pythagore;5
4;Jack;King;Geography;Oceans;10
```

#### Item Reader

L'item reader va être en charge de parser le fichier d'input (A) pour le découper en items (chunks) qui correspondront à la classe modèle que vous avez défini.

Mon modèle sera la classe : "StudentCsv" dans laquelle je vais indiquer les attributs que je veux récupérer et à quelle colonne ils correspondent dans mon fichier CSV.

```
public class StudentCsv {

    // id de l'étudiant
    private Long id;

    // Prénom de l'étudiant
    private String firstName;

    // Nom de l'étudiant
    private String lastName;
    
    // Matière
    private String area;
    
    // Nom de l'examen
    private String exam;
    
    // Note de l'étudiant
    private int note;
    
    // Ajouter getter/setter
    ...
}
```  

#### Processor (optionnel)



#### Item Writer


### Listeners



### Job et REST API



