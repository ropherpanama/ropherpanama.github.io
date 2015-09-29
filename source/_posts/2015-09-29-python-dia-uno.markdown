---
layout: post
title: "Python: Día 1"
date: 2015-09-29 16:12:06 -0500
comments: true
categories: python
---

### Aprender Python

Bueno, hace algunos días decidí hacer cosas con **Python** para ver que tal, ya que quería aprender un nuevo lenguaje y me decidí por él.
En mi caso venía de trabajar puramente con **Java** y para mi sorpresa las diferencias son muchas (jejeje lógico no?), pero hay unas que me agradaron muchas.

Visto desde el punto de vista de la **línea** de aprendizaje pues hacer un programa algo complejo (Conexión a base de datos con Oracle usando **ORM SQLAlchemy**) no me tardó mucho.

<!--more-->

Aunque atribuyo eso a que ya conocía un lenguaje orientado a objetos y que algunas cosas; pues son muy similares funcionalmente.

Si me percaté de **ciertas diferencias** muy notables que dejo a continuación:

1. **No tienes que "tipar"** (definir un tipo de dato) tus variables, el tipo de datos de las mismas es dinámico, es decir que según como la uses el tipo de dato de tu variable cambiará.
2. Los bloques de código **no se cierran con llaves**, en el caso del `for` y demás cosas por el estilo, se debe tabular el código (perfecto para mí porque tengo la tecla de la llave cerrando dañada :D)
3. Las funciones se declaran con la palabra **def** y aunque la función o método retorne datos no necesitas especificarlo en la definición de la función.
4. Debido a lo anterior y a lo del tipo dinámico de datos, la característica de POO sobre polimorfismo pierde un poco su lugar jejejjeeje.
5. Hablando de **métodos y constructores** todos (nunca se te olvide) llevan el parametro **self**, que es una forma como de **this** (de Java)
6. Para imprimir solo usa **print**!!! (no como ese largo `System.out.println` balalalalala .... )
7. Existe el **try/except** en vez de **try/catch**
8. Leer y escribir archivos ... qué les puedo decir ... **es muy fácil!**
9. Conectarte a una base de datos también es muy fácil, solo debes buscar los módulos indicados :)
10. La herencia es **multiple**!!! 
11. **No!** Los comentarios no inician con **//**, inician con **#**

Bueno y sobre eso un montón de cosas más que aún voy descubriendo, pero por lo general han sido cosas muy buenas e interesantes y se puede decir que ya le tengo cariño.

Antes de iniciar, pues lógicamente debemos [instalar](https://www.python.org/downloads/) **Python** en nuestra máquina para poder usar la **consola interactiva** (!Si, consola interactiva!)

Partí con **Python 3.3**, entiendo que va por la 3.4 (o quizá más adelante) pero bueno habrá que revisar, ya que mi primer tropiezo fué leer la documentación de **Python 2.x** y darme cuenta que el **print** se convirtió en un **método**, por ende se debía llamar con parentesis **print()**.

Para **Windows** es fácil, solo descárgate el instalador, lo instalas (valga la redundancia) y en tu menú de programas aparecerá **Python 3.3** (o la versión que instales), para mi fué más bonito usar la opción **IDLE** (Python GUI) que está dentro del menú **Python 3.3**, con este puedes ejecutar tu código presionando la tecla **F5**

Si te gustaría empezar con un IDE, pues [PyCharm](https://www.jetbrains.com/pycharm/download/) está muy bien.

Saludos!