---
layout: NoteLayout
permalink: /notes/:basename
category: notes
title: "Tests unitaires avec JUnit"
last_updated: "03/09/2023"
status: published
---

* TOC
{:toc}

On entend beaucoup parler de Test Driven Development (TDD) de nos jours. En pratique, sur mes projets, on était plutôt en mode NTDD (No Test Driven Development). C'est à dire qu'on faisait des tests unitaires si on avait le temps, comprendre rarement vu les deadlines qu'on nous impose. Puis un jour ils ont mis en place des règles de qualité avec Sonar imposant un taux de couverture minimum de 50%. Imaginez le drame. On ne pouvait plus livrer aucune feature à cause de ce blocage.

J'ai passé au moins 3 semaines (ok pas à temps plein mais quand même) à couvrir 1 an de code pour atteindre le taux de couverture. Parce que, en voulant atteindre ce taux de couverture, j'ai réalisé que beaucoup de méthodes n'étaient pas ou pas facilement testables (trop complexes, trop de dépendances, trop de void...). J'ai donc du faire beaucoup de refactoring pour simplifier et pouvoir tester plus facilement des petites portions de code et isoler ce qui était moins pertinent. 
En plus, c'était la première fois que je touchais à JUnit, le gros challenge.

Du coup cette note sera à la fois un partage de connaissances et un petit REX.

# Pourquoi les tests unitaires ? 

## Rapidité

On ne peut pas avoir plus rapide pour vérifier que son code marche. Je trouve que c'est encore plus vrai pour le dev back-end où l'on a pas forcément la possibilité de pouvoir tester en conditions réelles. 

De plus, tester en conditions réelles, j'entends sur un environnement local de dev, n'est pas toujours facile. Dans mon cas je travaille sur des logiciels qui sont en général installés sur des VM, certaines choses ne sont pas accessibles sur le PC en local, donc le moindre test nécessite un déploiement/installation sur la VM. Bref, les allers-retours entre les machines ça prend du temps juste parfois à cause d'une virgule.

Le test unitaire est donc un moyen rapide d'avoir un retour sur son code et d'identifier ses défauts.

## Maintenabilité

J'ai dû récemment faire des évolutions sur un code qui avait été fait y'a un an par une personne qui n'est plus sur mon projet. Bien évidemment il n'y a pas de documentation, heureusement il reste quelques commentaires dans le code. Néanmoins la tâche n'est pas simple, je trouve que l'architecture du code n'est pas limpide et j'ai mis beaucoup de temps à tout comprendre.

Ce qui m'a le plus aidé à comprendre ? Les tests unitaires. J'ai fait quelques petits tests sur des méthodes dans différentes classes pour comprendre le cheminement complet du code que je devais adapter. Le fait de rédiger le test et le faire passer m'a permis de valider que j'avais compris comment le faire marcher.

C'est aussi ça les tests unitaires, ça permet de laisser derrière vous un code maintenable, facilement compréhensible. Si tester le code est compliqué, c'est qu'il n'est pas fluide et qu'il sera dur à maintenir. Les tests vous aident à refactoriser et améliorer votre code pour assurer une meilleure maintenabilité.

## Prévention

Vous êtes surement tous déjà passés par là, quand on est beaucoup de développeurs à travailler sur une application avec beaucoup de nouvelles features, on rencontre rapidement la fameuse régression. 

Les tests unitaires peuvent permettre d'identifier plus vite les régressions. J'ai eu le cas sur mon ancien projet, je développais une nouvelle fonctionnalité ça marchait bien j'étais contente et là paf je vois que 3 tests ont planté. Sans m'en rendre compte ce que j'avais modifié avait eu un impact sur mes tests qui ne passaient plus. Je ne m'en serais pas rendue compte s'ils n'avaient pas été là. Ce qui m'a permis de corriger immédiatement et d'éviter un futur bug.

# Initiation à JUnit

Je vais essayer de vous faire un petit overview de ce qui peut-être utile à connaître en JUnit. On se basera sur JUnit 5.

## Les assertions

Le principe d'un test est de vérifier que le résultat renvoyé par votre méthode est conforme à l'attendu.

L'assertion est la méthode qui va vous permettre de valider votre test.

Il existe plusieurs types d'assertions qui vous permettront de tester différents cas. Je vais vous présenter les plus courants, en tout cas ceux que j'utilise le plus.

**assertTrue(result) / assertFalse(result)** : La plus simple, si vous avez une méthode qui renvoie un booléen (true/ false), il vous suffit simplement de lui passer le résultat de votre méthode pour qu'elle checke si la valeur est bien true ou false.

**assertEquals(expected, result)** : Si vous avez une méthode qui renvoie une valeur type String ou Integer par exemple, il vous suffit de lui passer en argument la valeur attendue et le résultat de votre méthode. Elle comparera les deux valeurs pour vérifier qu'elles sont identiques.

**assertThrows()** : On y pense pas forcément, mais il faut aussi tester les exceptions. Cette méthode vous permet de vérifier que l'exception est bien levée, qu'il s'agit de la bonne exception, et vous pouvez même pousser le vice un peu plus loin en lui demandant de vérifier que le message d'erreur renvoyé est bien celui attendu. Je m'en servais beaucoup pour tester les IOException par exemple le cas où une méthode doit utiliser un fichier et que le fichier ne serait pas présent à l'endroit spécifié.

**assertNotNull(result)** : Je l'aime moins celle-ci car elle insinue que vous êtes conscient que l'une de vos méthodes peut renvoyer null, ce qui n'est en général pas très bon signe, mais sait-on jamais elle peut servir. Vous l'aurez compris, elle permet de vérifier que le résultat renvoyé par votre méthode n'est pas null.

**assertAll()** : Je l'ai découverte assez récemment et je l'ai trouvé plutôt pratique. Par défaut si vous mettez plusieurs assertions dans une même méthode de test, le test va s'arrêter à la première assertion fausse et n'exécutera pas les autres tests. Si vous regroupez tous vos tests dans un assertAll, tous les tests de la méthode seront exécutés et il vous renverra tous les résultats même s'il y'en a un qui échoue.


## Les annotations

### Before / After

Dans une classe de test, vous trouverez 4 annotations vous permettant de pouvoir réaliser des actions avant ou après vos tests.

**@BeforeAll** : Cette annotation permet d'exécuter une méthode avant tous les tests. Elle ne s'exécutera qu'une seule fois au niveau de la classe.

**@BeforeEach** : Cette annotation permet d'exécuter une méthode avant chaque test. Elle s'exécutera autant de fois qu'il n'y a de méthodes dans la classe.

**@AfterAll** : Cette annotation permet d'exécuter une méthode après tous les tests. Elle ne s'exécutera qu'une seule fois au niveau de la classe.

**@AfterEach** : Cette annotation permet d'exécuter une méthode après chaque test. Elle s'exécutera autant de fois qu'il n'y a de méthodes dans la classe.


### Les pratiques

Je vous avoue que j'ai peu utilisé ces annotations, mais elles peuvent s'avérer pratiques.

**@DisplayName(" ")** : Cette annotation permet de changer le nom qui s'affiche dans votre console. Au lieu d'avoir le nom de la méthode, vous pouvez lui donner un nom plus explicite, pour décrire votre cas de test par exemple.

**@Tag(" ")** : Cette annotation peut vous permettre de filtrer vos tests pour ne relancer que les tests contenant le tag spécifié. Utile si vous voulez regrouper seulement les tests qui auraient des liens entre eux et ne pas tout relancer.

**@Disabled** : Cette annotation permet de désactiver un test pour qu'il ne soit pas executé. Ce n'est pas forcément conseillé mais dans l'éventualité où vous seriez amenés à rework une fonctionnalité vous pourriez avoir besoin de désactiver certains tests temporairement pour ne pas bloquer les autres développements.


## Générer vos tests dans votre IDE (Intellij Idea)

Petit tips pour la route. Vous le savez nos IDE sont là pour nous simplifier la vie.

Ils peuvent donc générer vos classes de tests pour vous.

Rendez-vous sur une classe que vous voulez tester (j'ai créé n'importe quoi pour l'exemple)

Faites un clic-droit sur le nom de la classe, vous verrez l'option "Generate" qui vous sert aussi pour les Getter/Setter

![generate](/assets/img/junit/GenerateTU.png "img-code")

Cliquez sur Generate, vous verrez que l'on vous propose "Test"

![generate-test](/assets/img/junit/GenerateTest.png "img-code")

Cliquez sur Test, vous verrez les différentes options qui s'offrent à vous
Vous pouvez cocher si vous souhaitez automatiquement ajouter des Before/After annotations et ensuite sélectionner les méthodes que vous vous voulez tester. Attention les méthodes "private" ne s'afficheront pas car elles ne sont pas accessibles.

![generate-method](/assets/img/junit/GenerateMethod.png "img-code")

Cela vous créera une classe de test que vous n'aurez plus qu'à compléter

![generated-class](/assets/img/junit/GeneratedClass.png "img-code")


# Pour aller plus loin

Si vous avez besoin de plus de détails, je vous conseille ces formations
* [JUnit 5 Fundamentals sur Pluralsight](https://app.pluralsight.com/player?course=3ecdec14-5806-4435-8bf2-aa9bca602379&name=e759196d-d0cf-4476-ab39-dfb70e4f3610)

Pour des tests plus complexes, vous pouvez utiliser ce qu'on appelle des Mocks. Pour faire simple vous "mockez" une classe pour qu'elle ne s'exécute pas pendant le test et à la place vous allez décrire le comportement attendu (ex : passer des valeurs fictives qu'elle est sensée renvoyer).
Cela vous permet de tester certaines méthodes qui peuvent faire appel à des services externes par exemple que votre test ne peut contacter (api, database etc...). Pour ce faire, vous pouvez utiliser Mockito.
