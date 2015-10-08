---
layout: post
title: "6 Python: Definiendo Clases"
date: 2015-10-08 13:50:22 -0500
comments: true
categories: python oop
---

Para este programa vamos a ver que tal se maneja el concepto de **Clase** con Python, revisemos línea a línea el siguiente programa para ver a que corresponde cada una.

> Como siempre te invito a copiar (a mano) las lineas que no tienen **#** por delante, ya que como sabemos son comentarios que el compilador ignora.

<!--more-->

Este programa escribirá todo lo que el usuario le envíe por consola en un archivo de texto, terminará cuando el usuario escriba **Adios**.

    #Una clase se define mediante la palabra clase class
    class Archivo:
    #Viniendo de Java lo primero que intente ubicar fue un constructor, en el caso de python, este se define como __init__, y algo muy importante es nunca olvidar
    #el parametro self, de olvidarlo veras algo como "TypeError: function() takes 0 positional arguments but 1 was given".
    #self viene a ser algo asi como el this de java, es decir los atributos de instancia que persisten a traves de la vida del objeto.
        def __init__(self, name, content):
            self.name = name
            self.content = content
            print("Archivo llamado ", name)
    
    #En java tenemos la palabra private para indicar que un atributo o metodo es privado, en python esto lo podemos hacer para los metodos con un doble subrayado, 
    #veremos que la forma de utilizar (llamar) estas funciones es un tanto diferente, no olvidar el parametro self
        def __escribir(self):
            t = input("Escriba > ")
            self.content += "\n" + t
    
    #Este metodo es normal, tal como lo habiamos visto en el programa 4
        def leer(self):
    #Validamos el contenido del archivo antes de leerlo
            if len(self.content) == 0:
                print("Archivo no tiene contenido, escriba algo")
            else:
                print("cat " + self.name + "\n",self.content)
    
    
    #Uso de la clase
    #Vamos a instanciar un objeto de nuestra clase
    #Recordar que arriba colocamos el metodo de inicializacion con los parametros de nombre del archivo y algo de contenido, notar que el self no debe ser cargado por 
    #nosotros
    a = Archivo("CV.doc", "")
    
    #Ofrecemos las instrucciones, notar que con triple doble comilla podemos imprimir lineas tal cual como las escribimos en el fichero de fuente.
    print("""Escriba:
        e para escribir
        l para leer
        bye para salir""")
        
    #Entramos a un blucle infinito, que se encargara de interactual con el usuario 
    while True:
        r = input("> ")
        if r == "bye":
            print("Adios")#Si el usuario escribe Adios salimos del programa
            break
        elif r == "e":
    #Observar el llamado a la funcion que definimos privada, a es el identificador de la instancia, seguido de un underline y el nombre de nuestra clase (Archivo) doble 
    #subrayado y el nombre de nuestra funcion.
            a._Archivo__escribir()#Llamado a una funcion privada
        elif r == "l":
            a.leer()
        else:
            print("Opcion no valida")
                 
         
Bueno, eso ha sido todo por hoy. Ya podemos definir clases, sabemos como instanciarlas y construir inicializadores según las necesidades de nuestro objeto.

Podemos acceder a funciones privadas y públicas de una clase.

Un saludo, bienvenidas son las preguntas!