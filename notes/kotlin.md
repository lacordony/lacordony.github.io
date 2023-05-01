---
layout: default
permalink: /notes/:basename
title: "Kotlin"
category: notes
published: false
---



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