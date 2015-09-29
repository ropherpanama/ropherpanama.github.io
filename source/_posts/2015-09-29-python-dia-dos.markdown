---
layout: post
title: "2 Python: Primer contacto"
date: 2015-09-29 16:14:29 -0500
comments: true
categories: python
---

Este fué mi primer programa con **Python**, muy simple realmente. Comento entre líneas lo que estaba haciendo (recordar que los comentarios inician con #)
Copia el contenido a continuación (te sería más instructivo escribirlo pero bueno ...) y pégalo en el **IDLE**, ejecútalo con **F5**

<!--more-->

    #*****************************************************************************
    #Mi primer programa Python
    #El print recibe cualquier cantidad de parametros separados por coma (,)
    #incluyendo expresiones aritmeticas como se muestra a continuacion.
    #Si se abre con IDLE, ejecutar con la tecla F5
    
    print ("Si sumas 2 + 3 el resultdo es ",
           2 + 3,
           "\nPero si los restas el resultado es ",
           2 - 3,
           "\nQue cosa no?")
    
    #Variables
    #No necesitas declarar de qué tipo son, sólo se declaran (tipo dinamico)
    a = "Soy una cadena de texto"
    b = 50
    c = 25
    
    print(a, "\nOperacion:", b + c)
    
    c = "Como los tipo son dinamicos, puedes cambiar el tipo de dato de tu variable en tiempo de ejecución"
    print(c) #Notar que c era un entero (25)
    
    multilinea = """ Esto es cool
                     puedo escribir lineas sin usar carracteres de escape
                     solamente usando las comillas triples :)"""
    
    print(multilinea)
    
    #Las cadenas tambien aceptan operaciones aritmeticas
    #Es decir que puedes multiplicar o sumar cadenas de texto
    d = "eco"
    e = d * 3
    f = "sistema"
    print("Multiplicacion de cadenas:", e)
    
    e = d + f
    print("Suma de cadenas:", e)
    #*****************************************************************************

**En resumen:**

Es bastante agradable el método **print**, ya que acepta lo que le pongas y como lo pongas (salvo el caso de los enteros y lo que no sea string. 

Pero tranquilo! tenemos el método **str()** que transforma a **string** lo que le pongas :) 

> Ej.: print(str(25))

Vimos que los tipos de datos son dinámicos (**c** era un entero y luego era un string)

Vimos los textos multilínea con `""" """"`, útil si no se quiere usar el clásico `\n` (que puede ser usado).
Y vimos la multiplicación de cadenas, por aquí nos vamos a ver que más encontramos con **Python**.

Un saludo! Cualquier duda, pues a la orden!