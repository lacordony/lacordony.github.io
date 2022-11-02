---
layout: default
category: notes
title: "Principes SOLID"
---

# Principes SOLID

Pour écrire cette note je me suis basée principalement sur ce cours : [Udemy - SOLID Principles: Introducing Software Architecture & Design](https://www.udemy.com/course/solid-design/learn/lecture/15983704#overview)

Les principes SOLID vous permettront d'avoir un logiciel bien conçu et robuste.


## S - Single Responsibility Principle (Responsabilité unique)

Chaque composant logiciel (classe, méthode, module) devrait avoir une et une seule responsabilité

Par exemple : un couteau suisse ne respecte pas ce principe car il dispose de multiples fonctionnalités, alors qu'un couteau simple n'a que pour fonction de couper.

Ce principe regroupe plusieurs notions :
* Cohésion : à quel degré les différents composants du sofware sont liés ?
Ex : si dans une classe avec plusieurs méthodes, certaines méthodes ne sont pas étroitement liées (finalités différentes) il vaut mieux les séparer dans 2 classes différentes qui leur donneront plus de sens.

* Couplage : quel est le niveau d’interdépendance entre différents composants du software ?
Ex : si dans une classe on retrouve le modèle de données et sa sauvegarde dans la base, la dépendance est trop forte. La donnée est étroitement liée au type de BDD ce qui n’est pas une bonne pratique. En cas de changement de BDD il faut tout changer.
A la place, on utilisera une classe repository qui aura la responsabilité de la BDD indépendemment du modèle de données

* Raison de changer : Chaque composant logiciel devrait avoir une et une seule raison de changer

## O - Open Closed principle (Ouvert Fermé)

Un composant logiciel peut être ouvert et fermé en même temps.

Par exemple : une console de jeu est fermée pour modification mais ouverte à des extensions (accessoires, manettes)

La solution pour répondre à ce principe peut-être de créer une interface permettant d’ajouter des implémentations sans impacter les autres dépendances

Il doit être facile d’ajouter de nouvelles fonctionnalités et des les ajouter sans ajouter de bugs et devoir faire de larges TNR


## L - Liskov substitution Principle LSP (Principe de substitution de Liskov)

Principe qui vient de Barbara Liskov

Les objets doivent être remplaçables par leurs sous types sans affecter l’exactitude du programme

Ce principe vise notamment à éviter les mauvaises pratiques en termes d'héritage (inheritance or is-A relationship).

Par exemple : Au premier abord une autruche est un oiseau, donc on aurait tendance à faire hériter la classe autruche de la classe oiseau. En pratique, cela pose problème car l’autruche ne peut pas voler donc la méthode voler ne peut pas être implémentée ce qui va entrainer des erreurs de tests et des bugs.

Il faut donc casser / adapter la hiérarchie pour qu'il n'y ai pas de méthode qui ne soit pas implémentable

S’il est nécessaire d’utiliser une condition telle que “if instance of” pour exécuter une méthode c’est qu’il y a un problème de conception

Pour vérifier que l'on applique correctement ce principe il faut appliquer la règle “Tell don’t ask” c'est à dire qu'il ne faut pas avoir besoin de demander une information pour exécuter une action


## I - Interface Segregation Principle ISP (ségrégation des interfaces)

Aucun client ne devrait être obligé de dépendre de méthodes qu'il n'utilise pas

Ce principe est assez similaire à Liskov mais appliqué aux interfaces.
Lorsque l'on crée une interface lors de son implémentation on s'attend à pouvoir implémenter l'ensemble des méthodes de cette interface. Si certaines méthodes ne sont pas implémentables car elles ne s'appliquent pas à notre use case on va être tenté de laisser la méthode vide sans implémentation car elle ne sera pas utilisée. Toutefois ce n'est pas une bonne pratique.

Pour répondre à ce problème, il vaut mieux diviser les interfaces et implémenter plusieurs interfaces en fonction du besoin.

Pour vérifier que l'on applique correctement ce principe on peut checker que l'on ne se retrouve pas dans les conditions suivantes :
* Grosses interfaces : les interfaces contiennent un trop grand nombre de méthodes 
* Faible cohesion : les méthodes de l'interface n'ont pas de cohérence entre elles, cela rejoint aussi le principe de responsabilité unique
* Implémentation vide : une méthode est implémentée à vide

## D - Dependancy inversion principle DIP (inversion de dépendances)

Les modules de haut niveau ne devraient pas dépendre des modules de bas niveau. Les deux devraient dépendre des abstractions.
Les abstractions ne devraient pas dépendre des détails. Les détails devraient dépendre des abstraction.

C'est le dernier principe et celui que je trouve le plus complexe à assimiler.

L'idée est de dire que l'on va privilégier des classes intermédiaires de type repository ou factory qui porteront les détails d'implémentation plutôt que d'aller instancier ou appeler directement les classes de bas niveau

Ce principe est lié à d'autres concepts qui peuvent aider à le comprendre :
* Injection de dépendances : consiste à injecter dans une classe ses dépendances afin de pouvoir passer la dépendance dans le constructeur de la classe plutôt que dans ses méthodes
* Inversion de contrôle IOC : consiste à déléguer la gestion de l'instanciation et l'injection des dépendances, celle ci se fait en amont au démarrage de l'application. Par exemple avec Spring l'annotation @autowired permet au framework d'instancier et injecter directement la dépendance dans la classe

