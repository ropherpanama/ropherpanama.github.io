---
layout: post
title: "Android, ListView dentro de un ScrollView"
date: 2015-09-29 11:32:20 -0500
comments: true
categories: android java
---

Aveces, cuando desarrollas **antes de leer las teorías** pasan cosas como esta.
Hace algunos días, me encontré con una dificultad al desarrollar una aplicación Android; mi caso era el siguiente.
Quería que una de las pantallas de mi aplicación respondiera a los cambios de orientación que el usuario realizara a su teléfono, esto no es mayor problema, por defecto el **manifest** de la aplicación configura todas las actividades para que esto suceda. Mi problema era que en esa pantalla tenia un `ListView` que desplegaba una lista de productos. En modo vertical se veía perfecto el `ListView`, pero al girar el teléfono; al ser el espacio vertical más pequeño, no mostraba todos los componentes de la lista, porque quedaban escondidos al girar la pantalla.

<!--more-->

**La solución:** Utilizar, en lugar de un `<LinearLayout/>` un `<ScrollView />`, el problema: 
> **NO SE PUEDE TENER UN LISTVIEW DENTRO DE UN SCROLLVIEW.**

Bueno ... con un pequeño truco si se puede, veamos:

**Mi actividad era algo así**

![enter image description here](http://4.bp.blogspot.com/-96MFYd6nWyk/UyvLJ4L7_QI/AAAAAAAAAIE/HwifvWIuSf4/s1600/cap1.PNG)

En lugar de tenerlo todo en un `LinearLayout`, debemos tener todo en un `ScrollView`, para que al girar el dispositivo podamos "scrollear" y poder ver todos los componentes de la GUI de la app.

Primero debemos crear nuestra propia clase que extienda de `ScrollView`

    package com.example.layout.modified;
    
    import android.content.Context;
    import android.util.AttributeSet;
    import android.view.MotionEvent;
    import android.widget.ScrollView;
    
    public class VerticalScrollView extends ScrollView {
    
      public VerticalScrollView(Context context) {
      super(context);
     }
    
      public VerticalScrollView(Context context, AttributeSet attrs) {
      super(context, attrs);
     }
    
      public VerticalScrollView(Context context, AttributeSet attrs, int defStyle) {
      super(context, attrs, defStyle);
     }
    
      @Override
     public boolean onInterceptTouchEvent(MotionEvent ev) {
      final int action = ev.getAction();
      switch (action) {
      case MotionEvent.ACTION_DOWN:
       super.onTouchEvent(ev);
       break;
    
       case MotionEvent.ACTION_MOVE:
       return false; // redirect MotionEvents to ourself
    
       case MotionEvent.ACTION_CANCEL:
       super.onTouchEvent(ev);
       break;
    
       case MotionEvent.ACTION_UP:
       return false;
    
       default:
       break;
      }
    
       return false;
     }
    
      @Override
     public boolean onTouchEvent(MotionEvent ev) {
      super.onTouchEvent(ev);
      return true;
     }
    }

Con esta clase reescribimos el comportamiento de un `ScrollView` normal, y esto nos evitará el mal funcionamiento de nuestra app al querer hacer scroll sobre la pantalla. Tal cual como esta allí pueden copiarla.
El siguiente paso será utilizar en nuestro **xml** de la actividad nuestra Custom Class, así:

![enter image description here](http://4.bp.blogspot.com/-3Gpr-xXwfko/UyvLmlj0FqI/AAAAAAAAAIM/ryRFTeXkw5Q/s1600/cap2.PNG)

Observar el inicio del tag del **xml** ahora, `<com.example.layout.modified.VerticalScrollView`, observar que es muy importante nombrar completamente la clase (nombre de paquete y nombre de clase) ,con esto estamos indicando que queremos usar nuestro **custom ScrollView** llamado `VerticalScrollView`, lo segundo es que he colocado el contenido de mi actividad dentro del nuevo `ScrollView`.

Con esto ya tendremos solucionado nuestro pequeño inconveniente y podremos Scrollear sobre un `ScrollView` que contiene un `ListView`.

Dudas a la orden, Saludos!