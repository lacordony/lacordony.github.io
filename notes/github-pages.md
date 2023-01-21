---
layout: default
category: notes
title: "Créer son blog avec Github Pages"
last_updated: "21/01/2023"
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

Le nom de votre repository doit respecter une certaine syntaxe pour qu'il soit reconnu en tant que Github Pages : ``<username>.github.io``

Pour plus de détails voir : [Créer son site avec Github Pages](https://docs.github.com/fr/pages/getting-started-with-github-pages/creating-a-github-pages-site)

### Installation et pré-requis

Pour développer votre Github Pages vous aurez besoin d'installer Ruby, Rubygems, Jekyll et Bundler.

#### Pré-requis

Pour ce faire je vous renvoie à la page [Quickstart](https://jekyllrb.com/docs/) qui est très bien détaillée, step by step. Il ne me semble pas nécessaire d'ajouter d'infos supplémentaires.

#### Configurer un thème

Comme je vous le disais au début, vous pouvez partir d'un thème tout fait pour vous faciliter la vie.

Pour installer votre thème vous trouverez la procédure ici : [Installer un thème](https://docs.github.com/fr/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)

En synthèse, il faudra :

* Ajouter le thème dans votre _config.yml, par exemple pour le thème Architect j'ai ajouté :

  ```config.yml
  remote_theme: pages-themes/architect@v0.2.0
  plugins:
    - jekyll-remote-theme
  ```
  
* Créer un fichier /assets/css/style.scss dans lequel vous ajouterez le CSS du thème via : 

![Github Pages Theme](/assets/img/github-pages/github-pages-theme.svg)

Je suis obligée de vous mettre une image sinon ma page interprète la syntaxe Liquid.

* Récupérer le HTML du thème que vous remplacerez dans votre fichier _layouts/default.html

#### Build son projet

Une fois votre projet installé et créé, vous pouvez le build pour voir le résultat en local via la commande :

``bundle exec jekyll serve``

Votre site sera accessible à l'adresse : [http://localhost:4000](http://localhost:4000)

### Déployer automatiquement son package pour publier son site

Vous pouvez choisir une branche à partir de laquelle sera automatiquement déployé votre site.

Par exemple, vous pouvez choisir de mettre en ligne uniquement la branche "main" de votre repository et travailler en local sur les autres branches.

Pour ce faire c'est très simple, juste un paramètre à configurer dans votre repository Github : [Publication à partir d'une branche](https://docs.github.com/fr/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

Attention à bien push votre projet à la racine du repo et non dans un sous-répertoire sinon Github pourrait ne pas réussir à le déployer et votre pipeline tombera en erreur.

```
username.github.io
|_ _layouts
|_ _includes
|_ _etc
|_ index.html
```

## Comprendre Jekyll pour customiser sa page

### Arborescence

Prenez le temps de vous familiariser avec [l'arborescence](https://jekyllrb.com/docs/structure/) du projet.

Il est important de comprendre dans quel répertoire vous devrez placer vos markdowns.


### Syntaxe Liquid

Liquid vous permettra d'ajouter un peu de logique dans vos pages HTML.

Je vous mets ci-dessous, une petite présentation des points les plus importants.

Si vous avez besoin de choses plus pointues, voici le lien vers la documentation : [Liquid](https://jekyllrb.com/docs/liquid/)

#### Les variables à moustache

Les variables doivent être écrites entre double accolade, appelée aussi moustache.

Vous en trouverez un exemple dans votre layouts default.html

![Github Pages Content](/assets/img/github-pages/github-pages-content.svg)

Je suis obligée de vous mettre une image sinon ma page interprète la syntaxe Liquid.

La variable <span class="keywords">content</span> est la plus importante, car elle représente le contenu de votre fichier markdown. C'est là que sera inséré votre texte dans la page.

#### Les boucles

Admettons que vous vouliez afficher dans votre menu ou une navbar la liste de vos pages.

Vous allez ajouter une boucle dans votre layout HTML :

![Github Pages Boucle](/assets/img/github-pages/github-pages-for.svg)


#### Les conditions

Admettons maintenant que vous ayez plusieurs catégories de page comme moi (blog, notes, portfolio).

Vous ne voulez afficher qu'une seule catégorie dans votre menu.

Vous allez ajouter une variable category en haut de votre fichier markdown

```
---
layout: default
category: blog
title: "Super titre"
---
```

Ensuite dans votre layout vous allez ajouter une condition pour ne filtrer que sur les pages de cette catégorie.

![Github Pages if](/assets/img/github-pages/github-pages-if.svg)

## Ajouter des plugins

Vous serez peut-être amenés comme moi à avoir besoin de choses qui ne sont pas présentes nativement dans jekyll.

Tout d'abord soyez vigilants sur deux points :
* Tous les plugins jekyll ne sont pas compatibles avec les Github Pages, vérifiez bien avant de vous lancer.
* Attention aux dépendances, vérifiez que votre version de jekyll est bien compatible avec la version de votre plugin

Pour l'exemple, j'ai voulu ajouter un plugin pour pouvoir insérer des emojis dans mes markdowns.

Pour ce faire, vous allez ajouter le plugin 'jemoji' à votre Gemfile :

``gem 'jemoji'``

Ensuite vous allez télécharger la dépendance via la commande :

``bundle install``

Et normalement en relançant votre application, ça devrait être ok.

Pour avoir une liste des emojis et leur syntaxe : [Complete list of github markdown emoji markup](https://gist.github.com/rxaviers/7360908)

Have fun !
