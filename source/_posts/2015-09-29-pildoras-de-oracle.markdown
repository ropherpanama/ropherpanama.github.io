---
layout: post
title: "Píldoras de Oracle"
date: 2015-09-29 15:20:01 -0500
comments: true
categories: oracle plsql databases
---

En este artículo publico pequeños tips relacionados a Oracle, PLSQL, configuraciones, etc. En fín, todo lo interesante que vaya encontrando.

<!--more-->

## 1. PLSQL SELECT INSERT

Hace algunos días tuve un apuro y me solicitaron crear un codigo en PLSQL para seleccionar datos de varias tablas y sintetizarlos (insertarlos) en otra.
Les muestro lo que me saco del apuro, saludos!

> Script válido para Oracle 

        Declare
           Cursor NOMBRE_CURSOR Is
                Select  
                SCAMPO_1, SCAMPO_2, SCAMPO_3
                From TABLA
                Where ... SI LO NECESITAN
                And ... SI LO NECESITAN
                .... MAS VALIDACIONES
           CUALQUIER_NOMBRE NOMBRE_CURSOR%Rowtype;
         Begin
           For CUALQUIER_NOMBRE In NOMBRE_CURSOR
           Loop
             Insert Into TABLA_DESTINO (CAMPO_1, CAMPO_2, CAMPO_3 ...) Values
               (CUALQUIER_NOMBRE.SCAMPO_1 , CUALQUIER_NOMBRE.SCAMPO_2, CUALQUIER_NOMBRE.SCAMPO_3 ...);
           End Loop;
         End;

Esto se puede ejecutar en algún SGDBD o desde un terminal.

## 2. ORA-01843: not a valid month

Si lo has intentado todo y nada te funciona, si revisas y revisas y todo está bien... haz esto:
Véte al `regedit`, en `Software` busca `ORACLE`, estando allí dale click a `KEY_XE` y según tu caso editarás el campo `NLS_LANG`.

Mi error se daba por esto:

    TO_DATE('1-Dec-2011 00:00:00','DD-MON-YYYY HH24:MI:SS')

Oracle no entendia el `Dec` (es que el mío no es gringo), el entiende `Dic`.

Puesto que en esa clave tenía este valor:

`LATIN AMERICAN SPANISH_PANAMA.WE8MSWIN1252`

Para "americanizarlo" coloca en `NLS_LANG` esto:

`AMERICAN_AMERICA.WE8ISO8859P1`

## 3. Exports Oracle

Podemos exportar datos con Oracle utilizando esta secuencia de comandos; solo debes reemplazar los valores `user`, `passwd`, `owner`, `file` y `log`.

En este caso solo estamos exportando los objetos de un esquema en particular (`owner`).

`exp user/passwd@sid owner=esquema file = nombre_archivo.dmp log=arch_log.log`

**En donde:**

* **user**: usuario de base de datos
* **passwd**: contraseña del usuario
* **owner**: dueño del esquema que vamos a exportar
* **file**: nombre del archivo de salida producto del export
* **log**: archivo en donde se almacenará toda la salida (debug) del proceso
 
Más info aquí: ["Artículo"](http://www.oracle-dba-online.com/export_and_import.htm "Import y Exports")

Seguro que esto va a ir creciendo. **Un saludo a todos!**


