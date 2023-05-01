---
layout: default
permalink: /notes/:basename
title: "Les variables"
last_updated: "10/12/2022"
category: notes
published: false
---

Une variable permet de stocker une donnée (= valeur) en mémoire pour qu'elle soit utilisée par le programme.

### Types de variables

Voyons quelques exemples de variables

| Type    | Valeur      | Déclaration                            |
|---------|-------------|----------------------------------------|
| String  | "mot"       | ``` String mot = "un mot"; ```         |
| integer | 1           | ``` int chiffre = 1; ```               |
| float   | 0.12        | ``` int chiffreCourt = 0.12; ```       |
| double  | 0.143545454 | ``` int chiffreLong = 0.143545454; ``` |
| boolean | true        | ``` boolean isMot = true; ```          |

La variable de type float est limitée en nombre de chiffres après la virgule et va tronquer le résultat, contrairement à double qui offre une plus grande précision.

Tu as peut-être remarqué qu'on écrit String en majuscule et int en minuscule.

Pourquoi on n'écrit pas Integer en majuscule ? C'est ce qu'on appelle <span class="keywords">l'autoboxing</span>

Pour résumer très succinctement le compiler java va automatiquement convertir la primitive en sa classe correspondante. 
Par exemple si vous écrivez int il effectuera un new Integer, si vous écrivez boolean il effectuera un new Boolean.

L'inverse existe également et s'appelle <span class="keywords">l'unboxing</span>.

### Nommage de variables

Le nommage des variables est important en développement. Il permet d'identifier explicitement ce que contient cette variable et de rendre votre code compréhensible par les autres.

Admettons que vous vouliez lister une liste de fruits.

Si vous appelez vos variables fruit1 et fruit2, c'est pas super clair.

``` Java
String fruit1 = "Pomme";
String fruit2 = "Poire";
```

Alors que si vous appelez vos variables comme le nom du fruit que vous voulez définir ce sera quand même plus lisible lorsque vous manipulerez vos données dans votre code.

``` Java
String pomme = "Pomme";
String poire = "Poire";
```

### Portée des variables

Qu'est-ce que la portée ? C'est le périmètre dans lequel votre variable va être visible et accessible.

Ce périmètre est en général un bloc de code (une boucle, une méthode, une classe).

