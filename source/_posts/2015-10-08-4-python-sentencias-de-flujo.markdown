---
layout: post
title: "4 Python: Sentencias de flujo"
date: 2015-10-08 13:41:01 -0500
comments: true
categories: python
---

Para el tercer programa, decidí fijarme en las sentencias de flujos (las más comunes), recomiendo revisar la [Documentación](https://docs.python.org/3/tutorial/controlflow.html) ya que hay muchas **cosas interesantes**.

Una de las cosas que puede llegar a romperte la cabeza son las identaciones del código que pertenece, por ejemplo a un `if`, `while`, `for`, etc. ya que al no requerir llaves para definir los bloques de código, debemos tener sumo cuidado con las **tabulaciones**.

<!--more-->

**No es lo mismo**

    for i in range(5):
    print(i)
    print("boo")

**que**

    for i in range(5):
        print(i)
    print("boo")

pueden ejecutarlo si gustan, en fin; otra cosa importante es recordar que los dos puntos **(:)** denotan el inicio de la sentencia de flujo, poner atención a ello en el siguiente código:
 
    #****************************************************************
    #Mi tercer programa Python
    #Si se abre con IDLE, ejecutar con la tecla F5
    
    #Sentencias de flujo
    
    #IF
    a = 10
    b = 70
    
    #Importante: las sentencias a ejecutar segun se cumpla la condicion o no; debe
    #identarse con un Tab
    if (b/a) > 5 :
        print("Alcanza para todos")
        print("tenemos", 70/10)
    else:
        print("No alcanza para todos")
    
    #WHILE
    #Se pueden omitir los parentesis de la condicion
    count = 0
    
    print("Uso del while")
    while ( count <= 5 ):
        count += 1
        print("Imprimo " + str(count) + " veces")
    
    #Entrada por teclado con input(""),
    #en Python 3 se elimino el raw_input()
        
    print ("While infinito, escribe adios para salir")
    
    while True:
        entrada = input("> ")
        if entrada == "adios":
            break
        else:
            print (entrada)
    
    #FOR
    #Similar a Java se puede iterar sobre objetos sin necesidad de un contador
            
    secuencia = ["uno","dos","tres","cuatro","cinco"]
    
    for e in secuencia:
        print("Salgo en " + e)
    #****************************************************************

**En resumen:**

Muy importante tener en cuenta los dos puntos **(:)** y las **tabulaciones** para los bloques de código, es vital esto, porque los métodos o funciones funcionan de igual forma.

Los que estamos acostumbrados a **C** o **Java** vamos; por inercia a utilizar **paréntesis** en las condiciones `if (1 == i)`, pero acá los puedes omitir `if 1 == i`

Vimos el uso de la función **str** (`print("Imprimo " + str(count) + " veces")`) sin esto no podríamos concatenar el entero al resto de la cadena.

Otra cosa importante, y que me tomó algo de tiempo darme cuenta, era que en **Python 3** se eliminó la función **raw_input()** para procesar la entrada del teclado, desde **Python 3.x** en adelante debemos usar **input()**

Descubrí que los **for** son bastante resumidos en comparación con otros lenguajes.

Recuerden revisar la [¡Documentación!](https://docs.python.org/3/tutorial/controlflow.html)
Saludos!