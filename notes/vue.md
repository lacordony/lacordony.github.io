---
layout: default
title: "Vue.js"
---

Je sais que je vous avais promis du java mais quelques connaissances front-end sont toujours bonnes à prendre.

Le front n'est clairement pas ma passion première mais c'est difficile aujourd'hui de se présenter en tant que développeur sans connaître aucun langage front. J'avais commencé un peu à me former sur Angular et React mais ils demandent beaucoup d'investissement pour les dompter, et je n'ai malheureusement pas ce temps. 

Vue se veut plus facile à appréhender donc si vous voulez des notions de front sans aller trop en profondeur, je pense que c'est la meilleure alternative.

## Installation

### Vue.js

La commande pour installer la dernière version de Vue

``` Vue.js
npm init vue@latest 
```

On va vous demander si vous voulez ajouter tout un tas de choses à votre projet, je vous conseille de mettre "No" partout dans un premier temps sauf si vous savez exactement à quoi cela correspond. Dans mon cas je n'ai ajouté que Vue Router. 

Ensuite vous pouvez lancer votre projet

``` Vue.js
cd <project-name>
npm install
npm run dev
```

[Documentation officielle : Créer une application Vue](https://vuejs.org/guide/quick-start.html#creating-a-vue-application)

### Bulma (optionnel)

N'étant pas une fan de CSS, j'utilise Bulma en complément pour aller plus vite.

``` npm
npm install Bulma
```

Vous devrez ensuite importer le bout de code suivant dans votre fichier <span class="keywords">main.js</span>

``` js
import 'bulma/css/bulma.css'
```

[Documentation officielle : Démarrer avec Bulma](https://bulma.io/documentation/overview/start/)


### Fontawesome icons (optionnel)

Si vous voulez ajouter des icons sur votre site, Vue supporte Fontawesome mais vous devrez installer quelques dépendances

``` npm
npm i --save @fortawesome/fontawesome-svg-core
npm i --save @fortawesome/free-solid-svg-icons

# for Vue 3.x
npm i --save @fortawesome/vue-fontawesome@latest-3
```

Vous devrez ensuite ajouter les dépendances dans votre fichier <span class="keywords">main.js</span>

Pour cela je vous renvoie vers l'exemple : [Documentation officielle : Ajouter des icones à votre projet Vue](https://fontawesome.com/docs/web/use-with/vue/add-icons)


## Développement

Je ne vais pas vous faire un copier/coller de la documentation, vous retrouverez sur cette page la documentation, le tutoriel et des exemples.

Je me contenterais dans cette rubrique de lister quelques exemples qui me semblent utiles.

## Déploiement avec Git et Netlify

Dans cette dernière partie, on verra comment déployer l'application sur Netlify
