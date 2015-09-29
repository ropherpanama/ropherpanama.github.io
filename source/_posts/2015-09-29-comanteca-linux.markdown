---
layout: post
title: "Comanteca Linux"
date: 2015-09-29 11:42:53 -0500
comments: true
categories: linux scripts
---
## Linux: comandos que me facilitan la vida!

Este post es simplemente para tener a mano comandos o secuencias de comandos que son muy útiles.

1. **Promedio del peso de los archivos en una carpeta, el peso se muestra en KB:**
*** *ls -l | gawk '{sum += $5; n++;} END {print sum/n/1024 " KB"}*
2. **Listar archivos con su peso en KB:** 
*** *ls -lh*
3. **Mostrar el total de archivos de una carpeta:** 
*** *ls | wc -l*
4. **Ejecutar un comando, ver la salida por terminal y a la vez guardarla en un archivo:**
*** *{comando} | tee salida.log*
5. **Buscar archivo a partir de un directorio en sus subdirectorios:**
*** *find . -name FILE.ext*

Esta lista se irá actualizando con más comandos útiles.
Saludos!
