---
layout: post
title: "7 Python: Conexiones a Base de Datos"
date: 2015-10-08 13:55:17 -0500
comments: true
categories: python oop oracle databases
---

Una parte importante y lo más real en casi todo entorno de trabajo automatizado, es la **interacción con una base de datos** (sea del tipo que sea). 
Para este fin **Python** nos ofrece una manera sencilla de trabajar con bases de datos.

<!--more-->

Debemos tomar en cuenta la versión de **Python** que estemos usando para instalar la líbreria específica para la base de datos que estemos usando.

> Usé Oracle XE 11g para este ejemplo

Vamos a ver un programa que realiza una tarea muy común:

1.  Conectarse a una base de datos
2.  Consultar una tabla
3.  Exportar los resultados a un archivo de texto

**Increíble** que esto lo podamos hacer con tan pocas líneas. Y en esta ocasión colocaré imágenes en vez de texto (**adiós copy/paste**) hahaha, veamos qué tal.

![enter image description here](http://1.bp.blogspot.com/-96Wm8t-t_zM/U4-UoRMgVwI/AAAAAAAAASA/6yCkRSNbdg8/s1600/Screenshot+-+04_06_2014+,+04_48_11+p.m..png)

Vemos que en las primeras líneas estamos haciendo un **import** de componentes externos, en este caso tenemos que instalas el módulo **cx_Oracle** que nos permite trabajar con bases de datos **Oracle**, para casos en que uses **PostgreSQL**, **MySQL**, **SQLite** deberás buscar el módulo adecuado y seguir los pasos de su instalación, tomar en cuenta que los módulos de base de datos van de acuerdo a la **versión de Python** que estés usando.

Otro punto importante es notar que podemos especificar un **name** a nuestro gusto (*cx_Oracle as ora*) eso ayuda cuando el nombre del módulo que importamos tiene un nombre muy largo.

Con **makedsn** construimos una cadena de conexión para el método **connect**, vemos que el primer parámetro es el **IP** del servidor de la BDD, segundo el **puerto**, y tercero el **nombre de la base de datos** (SID por ejemplo).

Una vez teniendo el **dsn** nos conectamos con el **user/password** de la base de datos.

Estando conectados podemos ejecutar **DML** y extraer datos, en este caso volcamos los resultados a un archivo de texto llamado **"tablares.txt"**

Al ejecutar el programa deberas ver lo siguiente:

![enter image description here](http://4.bp.blogspot.com/-gfnG_eVufwk/U4-Uok-NRSI/AAAAAAAAAR8/LugJRMIyqzM/s1600/Screenshot+-+04_06_2014+%252C+04_48_45+p.m..png)

En donde *11.2.0.1.0* es la versión de mi base de datos y seguido el tiempo que tomo el proceso en crear el archivo de texto con todos los registros.

Luego podremos ver que se ha creado el archivo de texto **"tableres.txt"**

![enter image description here](http://1.bp.blogspot.com/-B4SyMowJlLA/U4-UoqNY8CI/AAAAAAAAASE/RLkL-p_fDA8/s1600/Screenshot+-+04_06_2014+%252C+04_49_08+p.m..png)

Espero que les ayude, ya saben que bienvenidas son las preguntas!

Debemos estar de acuerdo en que para ambientes productivos, realizar una tarea como esta y en esta forma puede ser vista muy **"newbie"**, es decir; no es bien visto que escribamos codigo SQL
de plano en nuestro código y tampoco que una sola clase haga todo. Es importante modularizar, **Python** al igual que **Java** nos permite crear **"paquetes"** con diferentes módulos
que pueden encapsular tareas muy particulares pero que también son repetitivas. Como sugerencia para este tipo de procesos (conexiones a base de datos), he visto que me 
funciona muy bien usar un componente **ORM** como [SQLAlchemy](http://www.sqlalchemy.org/)

Un saludo!