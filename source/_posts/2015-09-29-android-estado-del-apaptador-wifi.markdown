---
layout: post
title: "Android: Verificar estado del WIFI"
date: 2015-09-29 11:35:21 -0500
comments: true
categories: android java
---

Este es un tipo de funcionalidad que es bueno tenerla en una clase de utilidades globales (en otras palabras, en una clase de métodos estáticos).

Aveces es necesario conocer el estado del adaptador de red WIFI, para permitirle al usuario o a la misma aplicación realizar o no un proceso crítico del flujo de ejecución.

Como lo escribí arriba, hagamos una **clase de utilidades**, como la siguiente:

<!--more-->

    import android.content.Context;
    
    public class SystemUtils {    
        public static boolean isWifiOn(Context context) {
            ConnectivityManager cm = (ConnectivityManager) context.getSystemService(Context.CONNECTIVITY_SERVICE);
            NetworkInfo ni = cm.getNetworkInfo(ConnectivityManager.TYPE_WIFI);
            
            if(!ni.isConnected()) return false; else return true;
        }
    } 

Nuestro método `isWifiOn` nos retornará un `true` si el WIFI está encendido; un `false` en caso contrario. Lo que nos permite implementar una acción dependiendo del caso en el que sea llamada la función, por ejemplo:

    if(SystemUtils.isWifiOn(getApplicationContext()))
		Toast.makeText(getApplicationContext(), "WIFI está encendido", Toast.LENGTH_LONG).show(); 
    else
		Toast.makeText(getApplicationContext(), "WIFI está apagado", Toast.LENGTH_LONG).show();

Noten que al ser un **método estático** lo podemos llamar sin instanciar la clase `SystemUtils`; pues lo podemos acceder mediante un llamado directo.

Otro punto muy importante, antes de ejecutar tu aplicación asegurate de que en el **AndroidManifest.xml** le estás cediendo los **permisos** a la aplicación para que pueda verificar el estado del adaptador.

    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> 

Espero les sirva, saludos!