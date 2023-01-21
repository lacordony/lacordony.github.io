---
layout: default
category: notes
title: "Créer son blog avec Github Pages"
last_updated: "20/01/2023"
---

Vous débutez, vous voulez quelque chose de simple à mettre en ligne comme un blog ou un petit CV en ligne.

Vous pouvez créer une Github Pages, c'est gratuit, facile et hébergé par Github.

Les Github Pages utilisent Jekyll (basé sur le langage Ruby) mais rassurez-vous, vous n'avez besoin d'aucune connaissance en Ruby pour y arriver. Vous aurez simplement besoin de quelques basiques : syntaxe Markdown, HTML/CSS, conditions (if/for).

Vous pourrez trouver à cette [page](https://pages.github.com/) une petite présentation et une explication très simple pour créer votre repository.

## Getting Started

### Choisir un thème (optionnel)

Ce qui est très pratique, si comme moi vous n'êtes pas un grand fan de front et de CSS, c'est que vous pouvez utiliser des thèmes prédéfinis pour démarrer que vous pourrez customiser par la suite.

Pour voir la liste des thèmes supportés vous pouvez vous référer à ce lien : [Liste des thèmes](https://pages.github.com/themes/)

Vous verrez que j'utilise par exemple le thème "Architect" que j'ai très peu modifié.

### Créer son repository Github

Le nom de votre repository doit respecter une certaine syntaxe pour qu'il soit reconnu en tant que Github Pages : ``<user>.github.io``

Pour plus de détails voir : [Créer son site avec Github Pages](https://docs.github.com/fr/pages/getting-started-with-github-pages/creating-a-github-pages-site)

### Installation et pré-requis

Pour développer votre Github Pages vous aurez besoin d'installer Ruby, Rubygems, Jekyll et Bundler.

#### Pré-requis

Pour ce faire je vous renvoie à la page [Quickstart](https://jekyllrb.com/docs/) qui est très bien détaillée step by step.

#### Configurer un thème

[Installer un thème](https://docs.github.com/fr/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)

#### Build son projet

Une fois votre projet installé et créé, vous pouvez le build pour voir le résultat en local via la commande :

``bundle exec jekyll serve``

Votre site sera accessible à l'adresse : http://localhost:4000

### Déployer automatiquement son package pour publier son site

[publication](https://docs.github.com/fr/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)


Attention à bien push votre projet à la racine du repo sinon Github n'arrivera pas à le déployer et votre pipeline tombera en erreur.



## Comprendre Jekyll pour customiser sa page

### Arborescence

Prenez le temps de vous familiariser avec [l'arborescence](https://jekyllrb.com/docs/structure/) du projet.

Il est important de comprendre dans quel répertoire vous devrez placer vos markdowns.


### Syntaxe Liquid

#### Les variables à moustache

#### Les conditions

#### Les boucles



Lien vers la documentation : [Liquid](https://jekyllrb.com/docs/liquid/)
