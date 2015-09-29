---
layout: post
title: "Introducción a Android con un ejemplo (y no es HelloWorld)"
date: 2015-09-29 11:27:28 -0500
comments: true
categories: android java
---

Esta introducción va a ser diferente, ya que no vamos a ver como instalar ni configurar el SDK o cosas por el estilo y vamos a pasar directo a ver como luce un proyecto de android una vez creado. Además vamos a aplicar algo de programación para hacer una ventana que haga algo más que el clásico HelloWorld.

Primero vamos a crear un nuevo proyecto de Android: **File -> New -> Android Application Project** (o sus similares en español).

Completa los datos como los ves en la siguiente imagen, los detalles de SDK van a depender de lo que tengas instalado en tu máquina, por lo general suelo definir como SDK mínimo el 2.3, para lo demás uso lo más reciente disponible que tenga; en mi caso el Target lo he colocado API 18 y compilaré
con el API 19

![enter image description here](http://4.bp.blogspot.com/-_4-FO8OZOYc/UzMj5-hW6KI/AAAAAAAAAIg/2uUpH37maNY/s1600/button_events_8.PNG)

Paso seguido vamos a asegurarnos de marcar las casillas que aparecen en la siguiente imagen:

![enter image description here](http://1.bp.blogspot.com/-lmkUUXZtaGs/UzMlcdv--JI/AAAAAAAAAJk/zbGNW0bP46M/s1600/button_events_9.PNG)

Desmarco **"Create custom launcher icon"** porque no me interesa ahora mismo crear un icono para la app.
Dejo marcada **"Create activity"** porque quiero que me genere y me configure una primera actividad (Pantalla y su controlador) que será la que editaremos más adelante. Presionamos Next

![enter image description here](http://3.bp.blogspot.com/-kipzblDykgY/UzMlcQzaynI/AAAAAAAAAJ4/qfYQUVlf2cU/s1600/button_events_10.PNG)

Como decidimos crear una **Activity** nos aparece esta pantalla, asegúrate de configurarla como en la imagen y presiona Next. En la pantalla siguiente colócale un nombre a tu activity (Activity Name), lo demás se autocompleta según lo que coloques. Presiona Finish.

![enter image description here](http://1.bp.blogspot.com/-S2ciCbhk_DU/UzMlcbf7flI/AAAAAAAAAJ0/Aas-vdl2PJI/s1600/button_events_11.PNG)

Después de seguidos estos pasos debes tener una estructura de proyecto como la siguiente:

![enter image description here](http://2.bp.blogspot.com/-KIEJi-lTiRA/UzMj8Bw0pCI/AAAAAAAAAI8/_nnl6I874hE/s1600/button_events_3.PNG)

Primero vamos a darle un vistazo al archivo llamado **AndroidManifest.xml**

Hay muchas cosas que no sabrás con qué se comen, pero por ahora lo que nos interesa conocer es lo siguiente:
1.  **Linea 4:** es la versión de nuestra app, la podremos ir aumentando según vaya creciendo nuestra app (nuevas versiones)
2.  **Lineas 13,14 y 15:** Si te fijas verás que la referencia a los componentes están precedidos por un **@**, esto significa que son recursos de tu aplicación, estos recursos pueden ser manipulados libremente por tí para personalizar tu app a tu gusto. Dáles un vistazo presionando la tecla **Ctrl + Click** sobre el **@** de cada uno.
3.  **Linea 17:** De esta forma se asocia la activity (XML) con tu código Java, ves que el **name del activity** es el mismo de la clase que se creó en el **package** que definimos (es su nombre completo **package + class name**)
4.  **Linea 19:** El `<intent-filter>`  en este caso está indicando que nuestra única activity que tenemos, será la primera en aparecer cuando ejecutemos nuestra aplicación, esto se logra con las lineas **20** y **22**.

![enter image description here](http://2.bp.blogspot.com/-RIoA1LMP-RM/UzMoR3HNGnI/AAAAAAAAAKE/4EcrxOlhuXw/s1600/button_events_6.PNG)

Ahora vamos a editar los ficheros **activity_button_event.xml** (archivo en donde se diseña la pantalla) y su controlador `ButtonEventActivity.java` (Que vendría siendo algo asi como el `Listener` del `JFrame` en `Swing`)

Primero editamos el xml para que en vez de un `TextView` (algo así como el `JLabel` de `Swing`) nos muestre un `Button` (algo así como el `JButton` de `Swing`), lo haremos de esta forma:

![enter image description here](http://3.bp.blogspot.com/-P74H8F4n6FY/UzMoR16fKEI/AAAAAAAAAKM/k4jQDWZWqjU/s1600/button_events_4.PNG)

Primero, hemos reemplazado el **Layout** (similar a como se aplican layouts en `Swing`) default por un `LinearLayout`, en la **linea 5** vemos que la orientación es **vertical**, esto quiere decir que todos los componentes que vayamos agregando se irán apilando **uno debajo del otro**.
En la **línea 12** estamos creando un `Button`, con su etiqueta o texto (Ver mensaje) y sus propiedades de tamaño, **fill_parent** le indica al componente que debe extenderse tanto como el tamaño de su contenedor y **wrap_content** le indica al componente que debe ajustarse al contenido que tenga el componente, en este caso es un texto, así que se ajustará al texto para extenderse.
En la **linea 16** se muestra la forma que ofrece **Android** para manipular los eventos de los botones (es muy sencilla y practica aunque no es la única forma), si venimos programando con **java SE** podremos aplicar los mismos mecanismos de manejo de eventos (`addActionListener` .. etc.). 

### ¿Cómo funciona esto?

Al definir en el `onClick` la etiqueta "`ejecutarEvento`", debemos crear en el controlador de la pantalla (archivo **.java**) una función sin retorno (**void**) con el mismo nombre de esa etiqueta y que reciba como parámetro un **View**, así de sencillo.

Veamos el código del controlador:

![enter image description here](http://3.bp.blogspot.com/-MzLU7JGUS9k/UzMoR_kp9DI/AAAAAAAAAKY/QSTIGgZ06yI/s1600/button_events_5.PNG)

Las primeras 24 lineas te las debe generar el **Eclipse** cuando creamos el proyecto, lo nuevo y lo que debemos añadir nosotros son las **líneas 29 en adelante** (sin olvidar escribir los javadocs, créanme que son muy útiles para quienes tengan que revisar su código posteriormente). Como se dijo, el nombre del método es el mismo al que tiene el `Button` en el `onClick` en el XML anterior y lleva un `View` como argumento.
Lo que hace nuestro botón es mostrarnos un `Toast` (un pequeño aviso en pantalla) indicando que se ha realizado un click en el botón.

Ahora puedes proceder a ejecutar tu aplicación, en la medida de lo posible usar un teléfono real, ya que el emulador suele ser muy lento :)

**Debe quedar algo así:**

![enter image description here](http://1.bp.blogspot.com/-lIKGAk40dis/UzMj8I1KvkI/AAAAAAAAAJA/_VeE9Tp-z_M/s1600/button_events_1.png)

**Y al presionar el botón debe aparecer esto:**

![enter image description here](http://3.bp.blogspot.com/-CxQOQQd5SOw/UzMj8cJauyI/AAAAAAAAAI4/kJegpZCGRGU/s1600/button_events_2.png)

Bien, eso es todo por ahora. En el próximo punto vamos a hacer que nuestra pantalla tenga más componentes, como `EditText` (algo así como los `JTextField` de `Swing`) y que lo que escribamos en ellos pase a otra pantalla para ser procesado.
Ahí, nos leemos. **Recuerda seguirme en las redes sociales**. Preguntas y comentarios a la orden, saludos!