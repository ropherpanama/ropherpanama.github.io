---
layout: post
title: "3 Python: Listas, Tuplas y Diccionarios"
date: 2015-09-29 16:17:16 -0500
comments: true
categories: python
---

Para el segundo programa vamos a ver las listas, tuplas y diccionarios.
En este punto existen varias cosas interesantes, como la **búsqueda por rangos**, la **búsqueda de atrás hacia adelante** en una lista, y la **búsqueda con saltos** (no sé como decirle exactamente). 

Vamos a verlo en el siguiente código.

<!--more-->

Cópialo y pégalo en el IDLE de Python y pínchale a F5.

    #****************************************************************
    #Mi segundo programa Python
    #Si se abre con IDLE, ejecutar con la tecla F5
    
    #Listas (arrays o vectores)
    lista1 = [1, 2, "tres", 4, "cinco", [2,3], 7, "ocho", "nueve", 10]
    
    print("Accediendo a la lista:", lista1[2])
    #La sublista esta en el index 5 de la lista principal, accedemos al primer valor
    #de ella (sublista)
    print("Accediendo a la sublista:", lista1[5][0])
    
    print("Lista original:", lista1)
    lista1[0] = 100
    print("Modifico 1er elemento (1 por 100):", lista1)
    
    #Uso de numero negativo (busqueda inversa)
    #Buscará la 3 posicion de atras hacia adelante de la lista
    print(lista1[-3])
    
    #Uso de Slicing (particionado) o busqueda por rango
    print(lista1[0:4])
    
    #Uso de saltos (cada n cantidad)
    #Buscara solo en la posicion 0 a la 8, saltando 3 elementos en cada item encontrado
    print(lista1[0:8:3])
    
    #Tuplas
    #Se pueden manejar a las listas
    #La gran diferencia es que las tuplas son inmutables
    #tupla1[1] = 100 (TypeError: 'tuple' object does not support item assignment) #este es el error que dá si intentas cambir algo, lo puedes descomentar para que lo vivas :)
    tupla1 = (1,2,3,4,5)
    print("Tupla:", tupla1[:3])
    
    #Diccionarios, la misma vaina que los HashMaps de JAVA :)
    diccionario = {"uno":1, "dos":2, "tres":3}
    print("Diccionario:", diccionario["uno"])
    
    #****************************************************************

**En resumen:**

Crear una lista es bastante sencillo, de igual forma acceder a sus elementos.

Si bien las tuplas pueden ser manipuladas como una lista para su consulta, la gran diferencia es que las tuplas son **inmutables**, es decir; que son como una especie de **constante**, no podemos cambiar los valores que les asignemos al crearlas.

Listas se crean con [], las tuplas se crean con ()

Y pues los diccionarios son una estructura de **clave = valor** en la que los valores se acceden por el nombre de la clave, similar a los **HashMaps** de **Java**.
De igual manera, aunque no lo puse aquí (y obviamente) podemos hacer pruebas de recorridos con un for, que por cierto lleva abreviadas muchas cosas para los que estamos acostumbrados a los **for** de **C** o los antiguos de **Java**.

Un saludo a todos!
