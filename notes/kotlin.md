---
layout: default
permalink: /notes/:basename
title: "Et si on passait à Kotlin ?"
category: notes
published: false
---


C'est quoi encore cette nouvelle lubbie ? Kotlin c'est un langage open-source développé par Jetbrains (ceux qui font Intellij) qui est compatible avec Java et peut-être utilisé pour tout type d'applications (back, front, mobile). En gros, il fait le café. 

Si je m'intéresse à Kotlin, c'est pour diversifier un peu mes compétences autour de l'écosystème Java et surtout parce que le développement mobile Android est quelque chose que j'avais beaucoup aimé en formation mais que je n'ai plus eu l'occasion de pratiquer. 

Etant donné que Kotlin a été fait pour rendre le développement Android plus facile et rapide, je me suis dit que c'était l'occasion de m'y mettre et peut-être retourner à mes premiers amours.

## Pourquoi Kotlin ?

Pour un développeur java, Kotlin a pas mal d'avantages :
- Compatible : Il est compatible avec Java, vous pouvez donc utiliser des librairies Java dans votre code Kotlin
- Concis : Il est plus concis que Java, il y a moins de code à écrire
- Fiable : Il est plus sûr que Java, il y a moins de risque d'erreur
- Mobile : Je l'ai déjà dit mais il permet de développer des applications Android plus facilement et rapidement









Convert java to kotlin : 
- Paste your java code into a .kt file, and IntelliJ IDEA will convert it to Kotlin automatically.
- With a Java file open in the editor, go to the main menu and select Code | Convert Java File to Kotlin File or press CtrlAltShift
0K

fun printHello () {
println ("Hello World")
}

printHello()

https://play.kotlinlang.org/

Variables 

val (final)
var can be changed
Can't change variable type int to string
Exclamation mark bang !! 
Elvis operator ?:

Null safety
?.

Strings
Can add variables in strings 
using $ 
"Hello $name"


Main
fun main(args: Array<String>) {
println("Hello World!")

        // Try adding program arguments via Run/Debug configuration.
        // Learn more about running applications: https://www.jetbrains.com/help/idea/running-applications.html.
        println("Program arguments: ${args.joinToString()}")
    }