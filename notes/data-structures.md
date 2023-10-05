---
layout: default
permalink: /notes/:basename
title: "Data structures"
category: notes
published: false
---

J'ai une angoisse dans la vie : les tests techniques. Les codingame, les leetcode, on m'a pas appris à farmer ça en formation. On avait fait un peu d'initiation à l'algorithmie ça m'avait fait chialer.

J'ai constaté que dans ces exos, c'était un peu toujours les mêmes concepts qui revenaient : les data structures.

J'ai plus le choix je suis obligée de repartir de zéro et tout revoir pour m'en sortir et pas passer 50min sur la lecture d'un énoncé leetcode et me sortir de cette frustration de "si vous savez pas faire ça, vous êtes un(e) mauvais(e) développeur(se)"

Pour m'aider, j'ai choisi le cours codecademy : [Pass the Technical Interview with Java](https://www.codecademy.com/learn/paths/pass-the-technical-interview-with-java)


# Linear Search

La recherche linéaire est sans doute la plus connue et la plus simple. Elle consiste à parcourir un tableau de données et à comparer chaque élément avec la valeur recherchée.

Imaginez que vous ayez une liste de toutes les séries et films que vous avez regardé sur Netflix ou autres. 
* Si le film que vous cherchez est en haut de votre liste, la recherche va être rapide. 
* Si le film que vous cherchez est en bas de votre liste, la recherche va être potentiellement beaucoup plus longue en fonction de la taille de votre liste. Si vous êtes comme moi grand consommateur de séries, ça peut être très très long.
* Si le film que vous cherchez n'est pas dans votre liste, vous allez devoir parcourir toute votre liste pour vous en rendre compte.

En conclusion la recherche linéaire va être plus ou moins efficace en fonction de la taille de votre liste et de la position de l'élément recherché dans cette liste.

