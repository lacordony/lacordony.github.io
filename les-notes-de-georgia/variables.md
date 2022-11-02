---
layout: default
category: notes
title: "Les variables"
---

# Les variables

Une variable permet de stocker une donnée (= valeur) en mémoire pour qu'elle soit utilisée par le programme

### Nommage de variables

Le nommage des variables est important en développement. Il permet d'identifier explicitement ce que contient cette variable et de rendre votre code compréhensible par les autres.

Admettons que vous ayez une classe Animal et que vous deviez instancier un chat et un chien.

Si vous appelez vos variables animal1 et animal2, on ne comprendra pas ce que vous instanciez.

``Animal animal1 = new Animal();``

``Animal animal2 = new Animal();``

Si vous appelez vos variables chien et chat, on comprendra ce que vous instanciez.

``Animal chien = new Animal();``

``Animal chat = new Animal();``

### Types de variables

Voyons quelques exemples de variables

| Type    | Valeur | Déclaration                       |
|---------|--------|-----------------------------------|
| String  | "mot"  | ``` String mot = "un mot"; ```    |
| integer | 1      | ``` int chiffre = 1; ```          |
| float   | 0.1    | ``` int chiffreVirgule = 0.1; ``` |
| boolean | true   | ``` boolean isMot = true; ```     |


Tu as peut-être remarqué qu'on écrit String en majuscule et int en minuscule.

Pourquoi on n'écrit pas Integer en majuscule ?
C'est ce qu'on appelle l'autoboxing.

En gros, le compiler java va automatiquement convertir la primitive en sa classe objet. 
Par exemple int deviendra Integer, boolean deviendra Boolean.
Pour nous ça change pas grand chose mais c'est bon à savoir.
