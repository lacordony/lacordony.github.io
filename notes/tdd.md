---
layout: default
permalink: /notes/:basename
category: notes
title: "Test-driven development"
last_updated: "24/09/2023"
published: false
---

Dans la note d'intro à [JUnit](/notes/junit), j'avais surtout parlé des annotations sans utiliser d'exemples concrets. Si comme moi, vous avez besoin de "voir pour le croire", je vous propose une note un peu plus concrète avec une introduction au TDD (Test-driven development).


# Aperçu de l'univers des tests

Maintenance 65% des coûts d'une application. Chaos, Connaissance limitée à peu de personnes, peu de validations

test valide la qualité (répond aux exigences) et performance avant l'utilisation

Pyramide de tests
Tests fonctionnels (d'acceptation) : validation utilisateur
Tests d'intégration : assure la compatibilité entre les différents composants de l'application
Tests unitaires : rapides

Black box
White box

Unit test : JUnit
Acceptance test : Selenium


Pratiques de tests
Injection de dépendances : injecter un objet dans l'objet qui en a besoin via le constructeur
Test doubles : remplacer un objet par un autre pour tester un comportement. stubs (remplace une réponse) and mocks  (comportement préprogrammé)

Bonnes pratiques
Tests doivent être lisibles et maintenables, doivent prévoir les cas passants et non passants

Anti-patterns
L'ordre des tests ne doit pas être important (pas de dépendances)
Les dépendances peuvent etre difficiles à identifier (fail en chaine)
Ne pas tester dans les détails, focus sur le résultat attendu et non le comment
Trop de couplage dans le code peut le rendre trop difficile à tester, si trop fastidieux il sera plus difficile à valider/délivrer


# Et le TDD, c'est quoi dans tout ça ?


Agile et TDD ne sont pas liés.
Ecrire les tests avant le code ? Pas nécessairement


red-green-refactor
Red : write test that fails
green : make the test pass
refactor : clean up, refactor

Why TDD ?
Pour le client
Valide les exigences/specs
Identifier les régressions plus rapidement
Réduit les couts de maintenance
Pour le développeur
Design first facilite architecture évite complexité inutile
Aide à voir les progrès et le reste à faire
Focus sur le besoin client et valeur apportée


Limitations
TDD ne répond pas à tous les besoins (vérifier le déploiement, changement de réseau, tests d'intégration). Performance, monitoring, sécurité
Support du management


# Le TDD en pratique

Avant de commencer, n'oubliez pas d'ajouter la dépendance [JUnit](https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api) à votre pom ou gradle.

Pour vérifier vos compétences en termes de tests et TDD, il arrive que les entreprises vous demandent de réaliser un kata. Un kata est un exercice de programmation qui permet de s'entrainer à un langage ou une technique. Vous retrouverez par exemple celui de la [calculatrice](https://codingdojo.org/kata/StringCalculator/).

Attention, je ne vais pas faire tout le kata dans cette note, je vais me baser sur le thème de la calculatrice pour illustrer les concepts.

## Qu'est-ce que je veux tester ? 

C'est la première question à se poser, quel est le résultat que je veux vérifier.

Admettons que l'on veuille développer une méthode qui va additionner 2 nombres. On veut donc vérifier que le résultat est bien égal à la somme des 2 nombres. C'est notre assertion.






# Pour aller plus loin

Si vous avez besoin de plus de détails, voici les formations qui m'ont inspirées cette note :
* [TDD : The Big Picture](https://app.pluralsight.com/library/courses/test-driven-development-big-picture-2022/table-of-contents) sur Pluralsight par @jolson88
* [Testez votre code Java pour réaliser des applications de qualité](https://openclassrooms.com/fr/courses/6100311-testez-votre-code-java-pour-realiser-des-applications-de-qualite) sur OpenClassrooms
* [TDD with JUnit 5](https://app.pluralsight.com/library/courses/tdd-junit5/table-of-contents) sur Pluralsight