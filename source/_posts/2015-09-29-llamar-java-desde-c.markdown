---
layout: post
title: "Llamando un programa en Java desde un programa en C"
date: 2015-09-29 16:05:15 -0500
comments: true
categories: java script unix linux c
---

> Vamos a usar un script para Linux/Unix, prueba con Windows y un bat a ver que tal

Intenté varias formas, al final me incliné por hacer un script de Unix y que éste contenga la serie de configuraciones que requiere mi programa Java; desde un programa en C, llamaremos al Script de Unix y éste llamará al programa Java.

<!--more-->

### Paso 1: Crear una clase

    public class Hola
    {
      public static void main(String []args)
      {
        System.out.println("I'm saying Helloooo!!!");
      }
    }

### Paso 2: Crear un Script (lo llamaremos "exe")

    url=`which java`
    
    $url Hola > salida
    
    if [ $? -eq 0 ]
    then
       echo 'El programa se ejecuto...'
    else
       echo 'El programa no se ejecuto'
    fi
    
    more salida


Guardar el archivo (yo le puse "exe") y darle sus respectivos permisos de ejecución `(chmod +x exe)`

### Paso 3: Crear el programa en C

    #include <stdlib.h>
    
    int main(void)
    {
       int result;
       result = system("exe");
    }

Como vemos, el programa en C ejecuta (con la función `system` ) el script `exe`, que es quién configura todo para que se ejecute nuestro programa java.

Compilar el programa java: 

    javac Hola.java

Compilar el C, **cc** es el compilador de C por defecto en sistemas **Linux**: 

    cc callJava.c (o el nombre que ustedes le pongan)

Salida de los programas:

    userhome/user/ejemplo> a.out
    El programa se ejecuto...
    I'm saying Helloooo!!!
    userhome/user/ejemplo>

A todos un saludo!