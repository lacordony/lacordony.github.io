---
layout: default
permalink: /notes/:basename
title: "Architecture logicielle"
status: brouillon
last_updated: "03/04/2023"
published: false
---

* TOC
{:toc}

Un jour, j'ai eu le "malheur" de dire que j'aimerais bien en apprendre un peu plus sur l'architecture technique/logicielle pour mon évolution de carrière. Entre ce que j'imaginais dans ma tête et ce qui a été compris par l'entreprise, ça a été deux mondes très différents. Je me suis retrouvée à suivre des formations sur la rédaction de solutions d'architecture pour des appels d'offres. Là où je demandais à progresser sur des compétences techniques plus pointues, on m'a envoyé faire du powerpoint et de la vente. 

Personnellement, j'ai un peu de mal à accepter l'argument du "tu n'as pas besoin de maîtriser la technique pour être architecte". Je suis une personne de convictions, je ne suis pas quelqu'un qui peut aller vendre une solution en laquelle je ne crois pas ou que je ne maitrise pas, c'est pas possible. J'avais ce même problème quand je faisais du recrutement des fois on me demandait de dire des choses aux candidats alors que dans ma tête y'avait une voix qui chantait "bullshit, bullshit~~". Juste non.

Du coup, je suis un peu dans une impasse, j'ai l'impression que ce que je demande c'est un genre d'OVNI. Puis par hasard total, je tombe sur ce cours d'OpenClassrooms : [Définissez votre architecture logicielle grâce aux standards reconnus](https://openclassrooms.com/fr/courses/7210131-definissez-votre-architecture-logicielle-grace-aux-standards-reconnus) et je réalise que c'est exactement le type de connaissances que je voulais acquérir. Quels sont les différents types d'architecture, comment elles fonctionnent, dans quels cas les utiliser ? C'est quand même pas la mer à boire ce que je demandais.

Cette note va être une très brève synthèse de ma compréhension de ces architectures. J'en ajouterais peut-être d'autres avec le temps et qui sait ça servira peut-être à ceux qui se poseront les même questions un jour.

## Architecture client-serveur




## Architecture pilotée par les événements (Event-driven)

Event 
Trigger
Behaviour

Event bus : canal de communication entre les users et les events
Event channel : canal auquel on peut souscrire pour etre informé de l'évenement
Event processing : effectue les actions une fois que l'événement est déclenché


## Architecture orientée services


