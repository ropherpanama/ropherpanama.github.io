---
layout: post
title: "Android Unable to execute dex: Multiple dex files"
date: 2015-09-29 11:38:22 -0500
comments: true
categories: android java jersey-json json
---

Este problema es bastante sencillo de solucionar, sólo hay que LEER (lo entendí después de una noche rompiendome la cabeza) en vez de GOOGLEAR.

**En mi caso el mensaje era este:**

> [2013-05-07 23:08:21 - Dex Loader] Unable to execute dex: Multiple dex files define Lcom/sun/jersey/api/json/JSONConfigurated;
> [2013-05-07 23:08:21 - smf-prototype] Conversion to Dalvik format failed: Unable to execute dex: Multiple dex files define Lcom/sun/jersey/api/json/JSONConfigurated;

Estoy trabajando en unos **webservices** que usan el soporte de **JSON** y para eso requiero un par de librerías.

<!--more--> 

La clave está precisamente en el mensaje :  
> com/sun/jersey/api/json/JSONConfigurated

Al buscar entre las librerías que estaba usando para los asuntos de **JSON** (`jersey-json-1.16.jar` y `jersey-bundle-1.17.jar`) me dí cuenta que ambos JARs tienen la clase `JSONConfigurated` ubicada en el mismo paquete.

![enter image description here](http://1.bp.blogspot.com/-e_SS03hFSSw/UYpjIpX6A1I/AAAAAAAAAD0/BVAwux4Dfp4/s1600/json+1.png)

![enter image description here](http://3.bp.blogspot.com/-5to6ccF1tbk/UYpjlQhgYwI/AAAAAAAAAD8/GQu0Dwe-ABo/s1600/json+2.png)

**Solución** : eliminar una de las librerías o usar un `bundle`, como en mi caso. En realidad sin saber había metido la otra librería (`jersey-json`) y por eso me tiraba el error, pero he visto en muchos lados que a la gente les pasa lo mismo con otras librerías.
Algunos borran las **Dependencias de Android** del **build path** (funciona pero si usas cosas como **anotaciones de Android** no es nada agradable), otros le hacen un simple **Clean** al proyecto, pero realmente el problema es este, debemos tener cuidado y control de las librerías que estamos incluyendo en nuestro proyecto, debemos fijarnos bien si las versiones que usamos son compatibles entre sí.

Un saludo! 