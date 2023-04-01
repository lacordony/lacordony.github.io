---
layout: default
category: notes
title: "Terminal et commandes Linux"
last_updated: "16/02/2023"
status: published
---

Première mission, j'ai dû utiliser une VM sous Linux, je n'avais jamais utilisé ça de ma vie. 

> "Dès que je voyais un terminal et des lignes de commande, c'était ma hantise."

J'ai appris sur le tas à l'arrache comme d'habitude, le traumatisme a fini par passer.

## Installer une distribution linux sur windows

Rassurez-vous ce n'est pas très dur.

Ouvrez une fenêtre Powershell en tant qu'administrateur et lancez cette commande :

```
wsl --install
```

Par défaut, vous aurez une distribution Ubuntu, si vous voulez en installer une autre je vous renvoie vers cette page : [Modifier la distribution Linux par défaut installée](https://learn.microsoft.com/fr-fr/windows/wsl/install)

Une fois l'installation terminée, redémarrez votre pc pour finaliser.

Le terminal ubuntu se lancera et vous demandera de choisir un username et un password. Ce user aura des droits administrateur.

Et en gros, c'est terminé.

Précision : ubuntu ne sera pas mis à jour automatiquement par windows, il faudra donc régulièrement mettre à jour votre version via la commande ci-dessous dans votre terrminal ubuntu :

```
sudo apt update && sudo apt upgrade
```

## Les commandes utiles

* Afficher le répertoire dans lequel vous vous trouvez :
```
pwd
```
* Afficher le contenu d'un dossier :
```
ls
```

* Afficher des infos supplémentaires sur le contenu d'un dossier : 
```
ls -l
```

* Se rendre dans un sous-répertoire :
```
cd <nom du répertoire>
```

Pour aller plus vite vous pouvez commencer à taper le début du nom du répertoire et utiliser tabulation pour compléter

* Créer un nouveau répertoire : 
```
mkdir <nom du répertoire>
```

* Créer un nouveau fichier : 
```
touch <nom du fichier avec extension>
```

* Déplacer un fichier dans un autre répertoire :
```
mv <fichier> <répertoire>
```

* Copier un fichier dans un autre répertoire : 
```
cp <fichier> <répertoire>
```

* Copier un répertoire et son contenu dans un autre répertoire : 
```
cp -r <répertoire cible> <répertoire destination>
```

* Supprimer un fichier :
```
rm <fichier>
```

* Supprimer un répertoire et tout son contenu :
```
rm -r <répertoire>
```

* Afficher le contenu d'un fichier :
```
cat <fichier>
```

* Afficher le contenu d'un fichier avec navigation : 
```
less <fichier>
```

* Chercher des éléments : 
```
grep <ce que je cherche> <où je le cherche>
```

## Besoin d'une formation quand même ?

* [OpenClassrooms : Apprenez à utiliser la ligne de commande dans un terminal](https://openclassrooms.com/fr/courses/6173491-apprenez-a-utiliser-la-ligne-de-commande-dans-un-terminal)
* [Udemy : Learn The Linux Command Line: Basic Commands](https://www.udemy.com/course/command-line/)

