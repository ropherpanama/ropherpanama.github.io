---
layout: post
title: "5 Python: Funciones"
date: 2015-10-08 13:46:44 -0500
comments: true
categories: python
---

Para el cuarto programa vamos a ponernos interactivos, vamos a crear un programa que nos diga nuestra edad, **muy sencillo**, pero nos servirá para entender mejor la captura de datos por teclado y lo más importante, definir y utilizar funciones (métodos).

Voy a **#comentar** todo entre líneas para que se entienda mejor.

<!--more-->

> Como de costumbre puedes escribir (**sí escribir**, no copy/paste) este código en tu IDLE de Python y ejecutarlo con F5

    #Mi cuarto programa Python
    #Si se abre con IDLE, ejecutar con la tecla F5
    
    #Funciones
    
    #Vamos a definir una fincion, su nombre es calcularEdad (a python no le gustan las mayusculas, pero es que vengo de Java entiéndanme)
    #Esta función o metodo va a recibir un argumento, fijense que no estamos especificando el tipo del argumento, simplemente va porque vá, queda de nosotros
    #manipular este dato en nuestro código, en este ejemplo; como lo vamos a recibir de input() por seguridad lo pasamos a string con str()
    #la función no retorna cosa alguna, solo nos imprime nuestra edad
    def calcularEdad (anio_nacimiento):
        print("Tu edad es " + str(2015 - anio_nacimiento) + " años")
        
    #la variable entrada tendra valor capturado por teclado, esto se logra con la función input()
    entrada = input("Ingrese su año de nacimiento ")
    
    #Vamos a llamar a nuestra función creada anteriormente con el valor que tomamos de entrada
    calcularEdad(int(entrada))
    
    #Bien, ahora que vimos funciones sin retorno (tipo void) vamos a ver funciones que retornen algo
    #nuevamente fue muy extraño para mi no tener la necesidad de definir qué es lo que debo retornar en mi función, simplemente con colocar la palabra return 
    #estamos indicando que la función retorna algo, en nuestro ejemplo retorna un entero (nuestra edad)
    def calcularEdad2 (anio):
        return 2014 - anio
    
    #Nuevamente vamos a tomar entrada desde el teclado para ejecutar nuestra función
    entrada2 = input("Ingrese su año de nacimiento ")
    
    #Vemos que para este caso, como la funcion retorna, podemos almacenar su valor retornado en una variable (answer)
    answer = calcularEdad2(int(entrada2))
    #Imprimimos la variable answer que  es la que posee el valor que retorno la funcion
    print("Tu edad es " + str(answer) + " años")
    
    #Numero variable de parametros en una funcion
    #Tal como lo indica la documentacion https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions
    #una funcion puede definirse para que tome una cantidad de argumentos variable, si bien es cierto en este ejemplo obligatoriamente estamos definiendo que 
    #se le deben enviar 2 argumentos (por arg1 y arg2), el tercer parametro puede ser una tupla o un diccionario, esto lo sabemos por el argumento *arg3.
    #Si la tupla no contiene valor alguno no se imprimirá nada que inicie con Item: o en el print de abajo, prueba colocarle algo a ver que pasa :)
    
    def variable(arg1, arg2, *arg3):
        for s in arg3:
            print("Item: " + str(s))
            
        print(arg1, arg2, arg3)
    
    
    a = input("Ingrese un numero ")
    b = input("otro ...")
    
    #array = [23,22,21,20] #lista extra #descomenta esta linea para enviarle una lista a la funcion
    #variable(int(a), int(b), array) # esta tambien si le pasas la lista
    variable(int(a), int(b))

**En resumen**

Muy importante y **si eres observador**, habrás notado que las funciones se definen con la palabra **def**.

Lo demás está explicado no?, las preguntas son bienvenidas!

Recuerden ir a descubrir mucho mas en la [Documentación](https://docs.python.org/3/tutorial/controlflow.html#more-on-defining-functions)

Saludos!
