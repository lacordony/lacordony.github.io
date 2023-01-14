# Domain-Driven Design (DDD)

L'objectif du DDD est de concevoir une application (et définir une solution technique) la plus pratique possible pour ses utilisateurs.

Pour écrire cette note je me suis basée surtout sur ce cours d'OpenClassrooms : [Appliquer le principe du DDD à votre application](https://openclassrooms.com/fr/courses/5647281-appliquez-le-principe-du-domain-driven-design-a-votre-application)

## Co-construire un modèle de domaine compris par tous

Vous l'avez surement déjà remarqué souvent le jargon utilisé par un utilisateur métier et un dévelopeur est différent. Pourtant, on parle de la même chose.

L'objectif du modèle de domaine, c'est de réussir à représenter un besoin d'une manière compréhensible par tous. 

Pour cela, il est nécessaire d'identifier des éléments clés qui pourront être regroupés par domaine.

Ces éléments clés ne peuvent être identifiés qu'avec le client qui possède le contexte et la terminologie.
Il est donc important de leur poser deux questions :
* Le "quoi" ? Quel est le produit, qui sont les utilisateurs ?
* Le "pourquoi" ? Que fait-on avec le produit ?

Un modèle de domaine peut avoir plusieurs domaines ou contextes délimités.

Le moyen le plus simple de construire ce modèle est d'utiliser un diagramme UML, mais pour ce faire il faut recueillir des informations

### Définir le besoin avec les experts métier

Il est important de poser le plus de questions possibles afin d'avoir une vision la plus précise possible de l'attendu :
- Que voulez-vous pouvoir faire ? = identifier les besoins
- Comment vous procédez à l'heure actuelle ? = identifier les processus
- Avez-vous besoin d'informations pour réaliser une action ? = identifier les pré-requis
- Est-ce qu'un événement déclenche cette action ? = identifier les déclencheurs d'événements (triggers)
- Quel est le résultat attendu ? = identifier l'attendu
- Que devrait-il se passer si ce n'est pas le résultat attendu ? = identifier l'inattendu

Attention, il est important de respecter la terminologie rapportée par les métiers. En tant que développeur on a tendance à utiliser le terme "utilisateur" pour désigner la personne qui va réaliser l'action, ce n'est pas précis et porte à confusion. En DDD, on se doit de respecter le langage métier pour qu'il soit compris par tous. 

C'est ce qu'on appelle <span class="keywords">l'ubiquitous language</span>.

Ce vocabulaire de domaine devra à la fin être partagé avec l'ensemble des parties prenantes (experts métier, utilisateurs, développeurs etc..) et validé.


