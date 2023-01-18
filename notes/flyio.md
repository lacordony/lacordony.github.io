# Déployer son application Springboot sur Fly.io

Cette note a pour objectif d'expliquer comment déployer son dockerfile sur fly.io

## Installer Fly sur Windows

Ouvrir Powershell et lancer la commande suivante :

``iwr https://fly.io/install.ps1 -useb | iex``

Se connecter à votre compte via la commande suivante :

``flyctl auth login``

Personnellement j'ai créé mon compte via mon compte Github

Source : https://fly.io/docs/hands-on/install-flyctl/


## 

Si vous ne savez pas comment générer votre docker file je vous invite à revoir la note sur Docker.

