---
layout: default
category: notes
title: "Spring Batch"
---

# Spring Batch

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

Je ne vais pas vous faire une demo de [Spring Initializr](https://start.spring.io/) ici, vous pouvez jeter un oeil aux dépendances qui peuvent être nécessaires dans ce [Pom.xml](https://github.com/GeorgiaLR/spring-batch-sample/blob/main/pom.xml)

### Avant-propos : versions de Spring

Lorsque j'ai suivi ma formation, nous étions en Spring version 2.7.1, j'ai constaté que certaines API étaient devenues deprecated depuis (JobBuilderFactory, StepBuilderFactory).

J'ai donc adapté les exemples ci-dessous en Spring version 3.0.1, dans mon repo git vous trouverez les exemples dans le package "lco.sample.app" mais vous pourrez toujours retrouver au besoin les anciens exemples dans le package "lco.training"

### Job

Commençons par le commencement, on a besoin d'un job.

#### Annotation et configuration

Pour espérer que quoi que ce soit ne fonctionne il est nécessaire d'ajouter à votre class main l'annotation suivante : `` @EnableBatchProcessing ``

Cette annotation va auto-configurer pour vous toutes les classes nécessaires au bon fonctionnement de votre job.

```
@SpringBootApplication
@EnableBatchProcessing
public class SpringBatchApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBatchApplication.class, args);
    }
}
```

#### Datasource

Important à savoir et à comprendre, un job a besoin d'une base de données pour stocker les informations relatives au job (son status, ses paramètres etc..)

Il faut donc lui fournir une datasource pour que le job repository puisse aller sauvegarder les informations dans la base de données.

Il est donc fréquent d'avoir 2 bases de données distinctes, une pour le fonctionnement de Spring Batch et une qui traitera les données que vous manipulez.




#### Job launcher




#### Job Parameters

#### Job Status




### Step : Chunk-oriented

![Spring Batch Chunk Schema](/assets/img/spring-batch/springbatch-chunk.drawio.png)


#### Item Reader

#### Processor

#### Item Writer


### Step : Tasklet


### Job et REST API

#### Annotation

### Listener

