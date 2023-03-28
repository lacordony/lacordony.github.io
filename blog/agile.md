---
layout: default
category: blog
title: "Agile yes, but..."
last_updated: "28/03/2023"
status: published
---

J'avais envie de faire un petit REX un peu second degré sur les méthodes agiles.

J'avais vu un tweet d'un gars qui disait refuser toutes les offres d'emploi qui mentionnaient les méthodes agiles. Il avait eu une mauvaise expérience sur le sujet et ne voulait plus travailler comme ça.

Beaucoup de personnes lui ont répondu que ce n'était pas l'agilité le problème mais plutôt la façon dont les personnes l'appliquait.

Je suis plutôt d'accord avec cette affirmation. En revanche dans son témoignage, je ne me rappelle plus en détails mais c'est vrai qu'il y'avait des trucs vraiment chelou.

> "Ce n'est pas la méthode le problème mais la façon dont les personnes l'applique"

J'ai eu la chance de voir plusieurs façons de faire : l'agilité très stricte et l'agilité désorganisée (ou chaotique)

Sur un de mes projets quand je suis arrivée ils faisaient de ["l'agile à peu près"](https://www.youtube.com/watch?v=8xXhD_kfP0s). En gros, ils faisaient un daily le matin, ils créaient des US dans jira qu'ils plaçaient dans un sprint et voilà c'est tout. C'était plus un mode un peu Kanban yolo, ce sera fait quand ce sera fait. J'avoue que ça m'a beaucoup destabilisée au début, moi qui venais d'un projet super strict en mode SAFe (Scaled Agile Framework).

On voit que c'est parfois difficile de trouver le bon compromis qui fonctionne et ça peut vite devenir un gros bordel.

## L'organisation

Très brève synthèse de ce qui se fait pour les novices.

Des équipes d'environ 8 personnes qui vont travailler sur des sprints (périodes de 2 à 3 semaines). Chaque sprint contiendra une liste de tâcher à réaliser et sera rythmé par un certain nombre de règles et de cérémonies.

Dans les équipes que j'ai connu on avait souvent 4 ou 5 dev (dont 1 tech lead), 2 ou 3 fonc/BA et 1 scrum master (+ le PO qui compte pas). Et rien que cette répartition déjà ça partait mal.

Dans le monde idéal on t'explique que les membres de l'équipe sont interchangeables, solidaires. Tout le monde peut aider ou se backup de façon à garder un rythme de travail constant quoi qu'il arrive (voir notion de vélocité).

En pratique moi je suis souvent tombée sur des équipes multi-sujets, c'est-à-dire qu'un dev travaillait sur un sujet, deux autres sur un autre sujet, un autre sur un autre sujet mais aucun de nous ne connaissait le sujet des autres. Du coup, le jour où t'étais pas là, personne ne savait traiter le ticket à ta place. C'est vraiment pour moi l'exemple même de ce qu'il ne faut pas faire. À savoir trop spécialiser les individus, au lieu de spécialiser les équipes. 

On s'est retrouvés complètement dépendants de personnes qui un jour sont parties et pouf toute la connaissance est partie avec eux, car les sujets étaient parfois tellement complexes et vastes que même en faisant une passation 1 ou 2 mois ce n'était juste pas suffisant pour être opérationnel. 

Avoir 2 personnes sur un sujet c'est pour moi le minimum vital et encore je trouve que ce n'est pas assez. Je me suis retrouvée plusieurs fois à partir en congés sachant qu'en revenant de congés tout serait resté tel que je l'avais laissé en partant car personne ne s'en occuperait. C'est franchement horrible comme situation, on dirait une espèce de prise d'otage, tu culpabilises de poser des congés parce que si y'a un problème bah personne ne saura s'en occuper. Alors que non, on ne doit pas se sentir responsables d'une mauvaise organisation, des moyens qu'on ne nous donne pas. 

Vous allez me dire "mais pourquoi vous n'avez pas formé pas des gens ?". Déjà j'ai mis du temps à avoir une 2ème personne et ensuite les deadlines étaient tellement tendues que livrer dans les délais et former quelqu'un en même temps c'était juste pas compatible. On nous laissait aucun moment pour "respirer" (certains étaient parfois sollicités pour bosser aussi le week-end) et de vraiment prendre le temps de faire du partage de connaissances, de la montée en compétences... C'était un rush permanent, un cercle vicieux.

Tout ça pour dire, quand vous mettez en place vos équipes, prévoyez des binômes/trinômes pour assurer la continuité de votre delivery et ne pas ajouter du stress/pression sur les épaules de vos équipes (qui ne vont pas rester dans ces conditions).

## Les concepts

Je vais surtout m'attarder sur les DOR et DOD qui sont pour moi deux concepts importants.

Ils portent le mot "Definition" cela signifie qu'il y a des règles à définir qui doivent être connues et partagées par tous.

### DOR - Definition of ready

Le DOR peut s'appliquer aussi bien aux features qu'aux user stories.

Le principe c'est de se dire "quels sont les critères qui me permettent de m'assurer que l'on peut commencer à travailler sur ce sujet ?"

L'objectif étant de s'assurer que les équipes de réalisation disposent de toutes les informations nécessaires pour réaliser leurs tâches.

Une fois que tous les critères sont définis, pour chaque feature/us on parcourt la liste et si tous les critères sont bien réunis, la feature/us est ready pour être embarquée par les équipes de réalisation.

En pratique (de mon expérience) tout le monde a l'air de s'en foutre. Soit y'a des critères, soit y'en a pas. Et s'il y'en a on va être très laxiste sur la vérification : "oui, oui c'est bon tous les critères sont réunis".

Et derrière, nous (les devs), on se pose plein de questions.

Est-ce que les critères sont trop exigeants, trop compliqués, pas assez généralistes ? Par qui ont-ils été choisis ? Sont-ils bien connus et partagés par tous ?

### DOD - Definition of done

Le DOD peut s'appliquer aussi bien aux features qu'aux user stories.

Le principe c'est de se dire "quels sont les critères qui me permettent de m'assurer que le sujet/la tâche est terminé(e) conformément à l'attendu ?"

L'objectif étant de valider le travail délivré par les équipes de réalisation. On peut avoir beaucoup de choses dans ce DOD : la qualité du code, la documentation, les tests réalisés (la validation des critères d'acceptation) etc... 

Une fois que tous les critères sont définis, pour chaque feature/us on parcourt la liste et si tous les critères sont bien réunis, la feature/us est passée à Done par exemple par le Product Owner (cela dépend de la chaîne de responsabilité de votre projet).

En pratique (de mon expérience), soit y'a trop de critères, soit y'en a pas. 

S'il y en a trop ça peut ralentir le processus de delivery, si on met 3 semaines à valider une US qui est développée depuis 2 semaines, qu'est-ce qu'on a raté ? À l'inverse si on ne met pas de critères, on prend de plus gros risques. Quels sont nos engagements ? Comment on se couvre vis-à-vis du client pour garantir que l'on a correctement répondu aux attentes ? Qui prend cette responsabilité en cas de problèmes ?

Mine de rien ce DOD c'est aussi une protection. Pas forcément besoin de 50 critères, définissez l'indispensable qui vous permettra de démontrer que vous avez répondu aux attentes. 

Souvent quand on parle de Jira aux devs ils ont un peu d'urticaire, on aime pas le blabla administratif. J'aimais pas au début non plus. Pourtant, avec l'expérience, j'ai vu que tracer c'était hyper important et Jira c'est super pratique pour ça. Plusieurs fois on a eu des soucis avec des clients et quand tu as des traces écrites ça te sauve la vie. 

Par exemple, j'aime bien décrire sur les tickets ce que j'ai testé avec des captures, tu montres ce qui t'a permis de valider que tu avais répondu à la demande. 

C'est déjà arrivé que le client nous reproche des bugs sur des fonctionnalités non demandées par exemple. Comment un truc qui n'existe pas pourrait marcher ? Je vous jure que ça arrive, vous n'êtes à l'abri de rien.

Alors protégez-vous (dans tous les sens du terme). 

## Les cérémonies

Aaaaaaaaaaaah ! Mon moment préfére ! (non)

On se plaint d'avoir beaucoup de réunions en France (et surement pas qu'en France) mais clairement les méthodes agiles ne nous ont pas rendu service sur ce point.

Je ne dis pas que ces cérémonies n'ont pas de sens ou sont inutiles mais clairement quand tu additionnes les cérémonies agiles + les réunions plus classiques (qui n'ont pas disparu pour autant, ne croyez pas ça) bin tu te sens pas productifs tous les jours. J'ai des journées où clairement je ne code pas et je fais du réunion teams. Franchement ça me gonfle.

### Le sprint planning 

À chaque début de sprint, on planifie une réunion pour faire la revue du backlog du sprint (à savoir ce qu'on s'est engagés à réaliser pendant le sprint), vérifier si tout est ok pour démarrer et se répartir les tâches.

Dans le principe ça a l'air facile. Dans les faits pas forcément, j'en ai vu qui duraient 2h voire une matinée.

En pratique, il arrive souvent que certaines tâches du sprint précédent n'aient pas été terminées pour x ou y raisons. Il faut donc reprioriser pour retirer du sprint ce qui ne pourra plus être embarqué si jamais on se rend compte que ça ne rentre plus dans la capacité. Ensuite, il arrive que l'on avait planifié de commencer un sujet à une certaine date car on attendait quelque chose en pré-requis et que ce que quelque chose qu'on attendait n'arrive finalement pas à la date prévue. On ne peut donc pas démarrer ce sujet qui va être reporté, il faut donc réajuster le planning et regarder quel sujet l'on peut traiter à la place.

Mine de rien tous ces aléas ça peut faire durer la réunion longtemps et devenir un casse-tête domino.

Ce que j'adore c'est que quand tu suis une formation sur l'agilité on te dit que chaque personne prend des tâches qui lui plaisent dans le backlog et la vie est belle. En fait non, il y a des projets où tu ne choisis pas on te dit "tu prends ça" et puis voilà. Certes tu peux toujours émettre des réserves mais si y'a que ça et que personne d'autre n'est dispo hein ! Have fun !

### Le backlog refinement (grooming)

Cérémonie que j'ai le moins pratiqué. Sur l'un de mes projets on la faisait en général en milieu de sprint (1h max) si des évolutions venaient à impacter le planning et les priorités.

En gros l'objectif c'est de faire le "ménage", de mettre au propre tout ce qui a eu des impacts sur le planning. Par exemple, le métier a remonté au PO qu'un sujet n'était plus d'actualités, on le retire du backlog. On a remarqué qu'un sujet avait été mal évalué et est plus complexe que prévu, on réestime on rajoute des US. Un nouveau sujet devient prioritaire il faut l'intégrer dans le planning et donc reprioriser etc...

On le pratiquait peu car il y avait en général peu de grosses évolutions, on les traitait au fil de l'eau sans vraiment passer par une cérémonie officielle.

### Le daily stand-up

Le plus connu. Tous les matins on se regroupe 15min et on synthétise brièvement les réponses aux questions suivantes : T'as fait quoi hier ? Tu vas faire quoi aujourd'hui ? Est-ce que tu as rencontré des blocages ?

Le but c'est de savoir un peu ce que chacun fait et de remonter les alertes pour pouvoir réagir vite et mettre en place les actions nécessaires.

Sur mon projet actuel on tient bien les 15 minutes et je trouve ça vraiment cool. Sur mon projet précédent c'était un cauchemar, avec certaines équipes il durait 45 minutes parce qui y'en a qui racontaient leur vie. Comme si leur journée d'hier elle avait duré une semaine.

Normalement ce qui se passe, c'est qu'il doit y avoir un time keeper pour faire un peu accélérer les gens et éviter de dépasser l'horaire. Pendant un moment, pour palier au problème, on avait bloqué un créneau de 30 min juste après le daily pour les sujets ad-hoc, si par exemple un sujet débordait pendant le daily on mettait un stop et les gens concernés restaient à la fin pour en discuter entre eux. Ce qui permettait de pouvoir libérer les autres et c'était vachement mieux.

En bref, le daily c'est bien quand c'est court (et pas à 9h, franchement c'est trop tôt non ?)

### La sprint review (démo)

LA DEMO ! Le truc que je déteste.

En général le dernier jour de sprint on fait la demo et la review. 

Pendant la démo on va présenter les sujets qui ont été finalisés et ensuite présenter un rapide bilan de ce qui a été réalisé. Par exemple le burndown chart, combien de tickets ont été "done", qu'est ce qui n'a pas été fait, quels ont été les blocages qui nous ont empêché de finir, les objectifs du sprint ont ils été atteints etc...

En moyenne ça peut durer 1h ou 2 selon le nombre de sujets à démontrer.

Personnellement c'est vraiment le truc que j'aime le moins en tant que dev, le côté présentation / powerpoint / bling-bling où on te demande de mettre des "effets wahou!" (ce que disait souvent un de mes anciens directeurs de projet). Quand tu taffes sur du parsing XML, l'effet wahou excuse moi, mais ?.. 

À un moment sur un de mes anciens projets on a décidé d'épurer un peu pour gagner du temps et donc de ne montrer vraiment que des fonctionnalités métier significatives pour s'éviter des trucs techniques qui font bailler tout le monde, donc on a laissé la main plus aux profils fonctionnels / business analysts de la team qui maitrisaient mieux aussi le jargon métier ce qui nous permettait de consacrer plus de temps à nos tâches techniques. Et franchement ça m'allait parfaitement ! 

### La retrospective de sprint

Ma cérémonie préférée (oui pour de vrai !) aussi appelée "bureau des plaintes". 

Je vais pas dire que j'aime me plaindre, mais qui n'aime pas ?

Le dernier jour du sprint, en général après la review, on fait une retrospective d'équipe. En moyenne je dirais que ça dure 1h30/2h si vous en avez gros sur le coeur.

L'objectif c'est de faire le bilan du sprint, y'a plein de façons de le faire certains le font via des mini-jeux parfois pour rendre le truc un peu plus détente/fun. Surtout que le sprint finit souvent le vendredi après-midi donc on aime bien finir sur un truc léger.

Ce qu'on veut savoir dans cette cérémonie c'est : qu'est-ce qu'on fait bien ou qui marche bien, qu'est-ce qu'on fait mal et qu'on veut améliorer, qu'est ce qui nous met des bâtons dans les roues et dont on veut se débarrasser (serial killer, un quoi ?). Une fois que tout le monde a exprimé ses B's and C's, on établit une liste d'actions à mettre en oeuvre pour éliminer ce qui fait mal (serial killer, un quoi ?)

Je trouve ça vraiment cool comme cérémonie car on peut s'exprimer et vraiment remonter les pratiques qui nous dérangent. Dans les faits, certaines choses n'ont pas toujours de solutions mais on arrive régulièrement à avoir quelques petites victoires. Et surtout on se rend compte que souvent on est plusieurs à partager les même ressentis ou frustrations donc ça fait plaisir de se dire qu'on est pas tout seul.

Bref, c'est la cérémonie "bon pour le moral"

Si vous voulez des exemples de mini-jeux pour vous aider à démarrer : [les 3 petits cochons](https://agile-tools.fr/3petitscochons/) ou [le bateau](https://agile-tools.fr/speedboat/).

Pour les jours de flemme, on se faisait un tableau tout bidon avec 3 colonnes du style : "encore, peut mieux faire, stop" et chacun mettait un gif dans chaque colonne pour illustrer son mood. C'était assez marrant.

Donc pour conclure je vais finir par un gif qui représentera les sprints

![Never Ends](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExOGJlYzZhZDU4MGM2YjZmODUzYTFhOTZiNWRhZjdiNmM0ODU0ZWNlOCZjdD1n/xT5LMzzuOJlH3yCcgw/giphy.gif)








