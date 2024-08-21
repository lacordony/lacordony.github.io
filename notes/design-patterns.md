---
layout: NoteLayout
permalink: /notes/:basename
title: "Design Patterns"
category: notes
published: false
---

* TOC
{:toc}

Je vous cache pas que les design patterns c'est un peu synonyme d'angoisse. J'en ai toujours entendu parler mais concrètement je les ai jamais vraiment vu sur le terrain. C'est un peu un mystère, ils sont peut-être là sans que je ne m'en rende compte.

L'objectif de cette note serait de mieux les comprendre, moins en avoir peur et comprendre comment ils peuvent nous aider.


## Introduction aux design patterns

### Pourquoi les design patterns ?

Les design patterns (ou patrons de conception en français) sont apparus en 1994 dans un livre écrit par le Gang of Four (GOF pour les intimes).

L'objectif de ces patterns est de fournir une solution nommée et réutilisable à un problème récurrent.

On le dit souvent en dev, il faut éviter de réinventer la roue. C'est un peu le principe. Ces patterns répondent à des problèmes que rencontrent régulièrement les développeurs au quotidien en proposant un design flexible,maintenable, réutilisable et surtout compréhensible par tous.

Il existe 3 grandes catégories de patterns :
- Creational : création et instanciation des objets
- Behavioral : interaction et distribution des responsabilités entre les objets
- Structural : création de structure, assemblage et relations



## Les patterns de création (creational)

Un bon point de départ. Comment vais-je organiser mes classes pour créer efficacement mes objets ?

On aurait tendance à se dire, bah je crée ma classe je l'instancie avec un new et no big deal. Alors pourquoi un pattern ?

Regardons quelques exemples ci-dessous.

### Singleton

Le pattern très probablement le plus connu et je pense le plus simple à comprendre, le singleton.

C'est simple : il consiste à ne créer qu'une seule instance d'une classe donnée. Vous le voyez en général souvent dans les composants Spring (Bean), les classes sont instanciées une seule fois au démarrage du serveur. Vous l'avez également croisé si vous avez utilisé des loggers.

La particularité du Singleton est que son instance et son constructeur sont privés, de façon à ce que personne ne puisse réinstancier l'objet.

Pourquoi l'utiliser ? 

Il peut-être pratique lorsque vous avez besoin de communiquer des informations à la globalité de votre application sans avoir à systématiquement réinstancier un nouvel objet qui contient la même chose. Par exemple, des paramètres de configuration.

Pourquoi ne pas l'utiliser ? 

Cette solution n'est pas "Thread Safe", il est important de bien comprendre quand et comment vous utiliserez votre classe si celle ci contient notamment des attributs de classe amenés à changer. Si vous l'appelez deux fois en parallèle et que vous changez des valeurs attributaires, cela impactera les deux appels.

### Builder



Avoid big constructor with many attributes
Some setters can be let empty, inconsistency
.Builder.with(...).with(...).build()


### Factory et Abstract factory

Les patterns de factory ont pour but de gérer la création des objets. Comme leur nom l'indique, ce sont des petits usines à objets.




## Les patterns comportementaux (behavioral)



Strategy and state pattern

### Strategy : Plan or approach or algorithm
Multiple strategies with same input and output can have many implementations
Create an interface to implement each strategy
Context classe
With the state the principle is same you can encapsulate the state in abstract or interface to represent all possible states and define behavior for each state

 ### Command
Command super type  encapsulate different command methods
Invoker setCommand and carry the request

### Observer
Notify one or many subscribers when something change in publisher
Observer classe implements by other classe that needs to be notified

### Template Method
Series of instructions/steps to execute


## Les patterns structurels (structural)

### Facade
Simplified interface 
Doesn’t encapsulate
Delegate client request to existing subclass

### Decorator
If an object needs dynamic construction
Ex adding toppings to pizza can’t be anticipated 
Recursive calls to decorators

### Adapter

### Proxy
Proxy class to not refer to real class
Control access to the object
Security / Cache




## Synthèse





Pour aller plus loin : 

- https://refactoring.guru/fr/design-patterns/catalog
- https://openclassrooms.com/en/courses/5684096-use-mvc-solid-principles-and-design-patterns-in-java
- https://www.pluralsight.com/courses/java-design-patterns-big-picture
- https://www.coursera.org/learn/core-java-design-patterns
