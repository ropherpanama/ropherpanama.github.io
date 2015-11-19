---
layout: post
title: "Mismo resultado, distintas Bases de Datos"
date: 2015-11-19 09:43:00 -0500
comments: true
categories: oracle mysql sqlite postgresql
---

Aveces cuando se trabaja con varios tipos de bases de datos olvidas o confundes como obtener un determinado resultado o cómo se hace algo muy específico, pasa mucho con las funciones como obtener la fecha y hora del
momento justo, entre otras cosas. A continuación detallo una tabla con los sistemas de gestión de base de datos que utilizo frecuentemente; ya que aveces lo olvido.
<!--more-->
Ordeno el cuadro; en el orden en que personalmente uso cada gestor; siendo PostgreSQL el que menos uso (pero realmente lo uso mucho) 

Lo comparto :) 

| Objetivo                   	| Oracle                                        	| MySQL                                    	| SQLite                        	| PostgreSQL                              	|
|----------------------------	|-----------------------------------------------	|------------------------------------------	|-------------------------------	|-----------------------------------------	|
| Hora y fecha del momento   	| sysdate                                       	| now(), current_timestamp                 	| datetime()                    	| current_timestamp                       	|
| Añadir n meses a una fecha 	| add_months(to_date('20151225','YYYYMMDD'), 3) 	| date_add('2015-12-25', interval 3 month) 	| date('2015-12-25','+3 month') 	| date('2015-12-25') + interval '3 month' 	|
|                            	|                                               	|                                          	|                               	|                                         	|