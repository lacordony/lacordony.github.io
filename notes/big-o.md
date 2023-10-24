---
layout: default
permalink: /notes/:basename
title: "Big O Notation"
category: notes
published: false
---

L'algorithmie, c'est quelque chose qui m'a donnée beaucoup de fil à retordre durant ma formation. On ne m'avait jamais parlé de la notation Big O et du coup j'ai un peu de mal à l'assimiler.

Pour faire simple, c'est un moyen de mesurer la complexité d'un algorithme. En fonction de la complexité, on pourra choisir une solution plutôt qu'une autre pour la résoudre. Elle permet notamment d'aider à optimiser notre code pour qu'il soit plus rapide et plus performant.

L'objectif de cette note va être d'essayer d'expliquer simplement ce qu'est la notation Big O et comment l'utiliser.

## Y'a quoi dans ce Big O ?

Il se base sur deux notions importantes :

1. Complexité de temps (Time complexity)

Combien de temps le code met à s'exécuter.

2. Complexité d'espace (Space complexity)

Combien de mémoire le code utilise.

## Identifier les scénarios

Pour identifier la complexité d'un algorithme, il faut identifier les scénarios possibles. 

En général, on identifie 3 scénarios :
- le meilleur scénario (omega)
- le scénario moyen (theta)
- le pire scénario (omicron)

Par exemple, si on prend un tableau de nombres ci-dessous :

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|----|

Le meilleur scénario serait que le nombre que l'on cherche soit le premier du tableau (1), le pire scénario serait qu'il soit le dernier (10).
Le scénario moyen serait que le nombre de l'on cherche soit celui du milieu (5).

## Notations 

### O(n)

La notation O(n) est la plus simple. Elle signifie que le temps d'exécution de l'algorithme est proportionnel à la taille de l'entrée.

Par exemple, si vous bouclez sur notre tableau précédent n correspond au nombre d'itérations sur laquelle vous allez boucler.
Plus le chiffre sera grand, plus l'opération sera longue.




## Graph de synthèse

Pour finir cette note, voici le petit graph de synthèse qui résume les notations Big O en fonction de leur complexité de temps et d'espace.

![Big O Graph](/assets/img/big-o-graph.png "img-big-o-graph")


