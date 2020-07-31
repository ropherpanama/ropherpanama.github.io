---
title:  "Spring Boot Actuator"
date:   2020-01-08 15:04:23
categories: [spring-boot, java, actuator]
tags: [spring-boot, java, actuator]
---
Dentro de las tareas básicas de desarrollo e implementación de un componente de software está, la vital tarea de monitorear el comportamiento, rendimiento y demás indicadores que nos proveen información sobre el desempeño de nuestro software en un ambiente productivo.

Los actuators de Spring nos permiten obtener los beneficios de un sistema de monitoreo con configuración mínima. Sin demasiadas líneas podemos tener acceso a diferentes métricas sobre nuestra aplicación; disponibles 
a través de JMX o HTTP y con la posibilidad de utilizar herramientas adicionales para una mejor presentación de ésta información.

Lo que debes hacer para iniciar a jugar con esto:

1. Crea o genera un proyecto Spring Boot, en mi caso utilizaré la herramienta web de generación de proyectos de Spring Boot, dentro de las dependecias
que voy a incluir están: Spring Web, Spring Boot Actuator, Prometheus (para uso más adelante) y Lombok

    ![](/jekyll-uno/images/spring-boot-actuator/1.png)

2. Importa el proyecto en STS o Eclipse y sin realizar modificación alguna en el proyecto; abre un terminal en eclipse y ejecuta 
el comando **mvn spring-boot:run**. Notarás en la salida del terminal que se indica que se están exponiendo 2 endpoints sobre el path **/actuator**.
Estos endpoints son generados por la dependecia Spring Actuator que incluimos durante la generación del proyecto.


    ![](/jekyll-uno/images/spring-boot-actuator/2.png)

3. Probemos los endpoints, para esto voy a usar **Postman**: En mi caso la aplicación esta desplegada en el puerto 8080 de mi equipo, por lo que 
al ingresar en Postman un request de tipo **GET** al URL *http://localhost:8080/actuator* obtengo la siguiente respuesta

    ![](/jekyll-uno/images/spring-boot-actuator/3.png)

    Por defecto se exponen los endpoints **health** e **info**, pero debes saber que existen otros endpoints que deben ser configurados
    para exponerlos y que aparezcan en esta consulta. Puedes ver todos los endpoints en la documentación de [Spring Boot Actuator](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-features.html#production-ready-endpoints) para que tengas
    más detalle.

4. Probemos uno de los endpoints, a ver el **health**

    ![](/jekyll-uno/images/spring-boot-actuator/4.png)

    Este endpoint lo podemos utilizar para conocer el status de la aplicación, por defecto solo muestra la palabra **UP**, más adelante veremos 
    como configurarlo para que nos dé un poco más de información.

5. Configuremos la aplicación para que nos muestre todos los endpoints disponibles: abre el archivo **/monitoring/src/main/resources/application.properties**
y agrega la siguiente línea:
    
    management.endpoints.web.exposure.include=*
    
    El * significa que estamos exponiendo todos los endpoints disponibles, de otra manera (separando por comas los endpoints deseados) 
    también podemos seleccionar los endpoints que puntualmente nos interesa exponer. Reinicia la aplicación y vuelve a cargar el request hacia **/actuator**. Observa que
    esta vez la cantidad de endpoints expuestos son 14.

    ![](/jekyll-uno/images/spring-boot-actuator/5.png)
    
    Al recargar la aplicación y ejecutar nuevamente la consulta en el Postman vas a observar el siguiente listado
    
    ![](/jekyll-uno/images/spring-boot-actuator/6.png)
    
6. Vamos a crear un Controller y un pequeño POJO en nuestra aplicación para exponer un servicio web sencillo
    
    **POJO Tutorial (usamos anotaciones de Lombok)**

    ![](/jekyll-uno/images/spring-boot-actuator/12.png)

    **Controller Tutorial**
	
	![](/jekyll-uno/images/spring-boot-actuator/13.png)
	
7. Probemos el endpoint **/actuator/beans** y ubiquemos el controller Tutorial
    
    ![](/jekyll-uno/images/spring-boot-actuator/7.png)
	
	Vemos que este endpoint nos permite obtener un estado de los beans que forman parte de nuestra aplicación, entre otras posibilidades.
	
8. Configuremos el endpoint **health** para que nos brinde más información, esto lo hacemos colocando la siguiente línea en el archivo properties de la aplicación

    management.endpoint.health.show-details=always
	
	![](/jekyll-uno/images/spring-boot-actuator/8.png)
	
	Reinicia la aplicación y ejecuta nuevamente en **GET** hacia el endpoint **health**, observarás lo siguiente
	
	![](/jekyll-uno/images/spring-boot-actuator/9.png)
	
9. Por último configuremos la información que debe aparecer en el endpoint **/info**, para esto colocaremos las siguientes líneas en el mismo archivo properties

    ![](/jekyll-uno/images/spring-boot-actuator/10.png)
	
	Reinicia la aplicación y observa lo que se despliega en la respuesta
	
	![](/jekyll-uno/images/spring-boot-actuator/11.png)

Ciertamente es interesante todo lo que nos ofrece esta funcionalidad dentro de Spring, de mi parte queda el tema de conocer cuáles son los impactos (quizá los negativos)
 que puede provocar este tipo de "Magia" que ocurre sin nuestro control. Temas de rendimiento y demás.

Lo siguiente debería ser utilizar **Prometheus** para observar esta información en un formato más leíble y explorable, luego quizá verlo con algo como **Grafana**.

Te dejo el repositorio de codigo en [Github](https://github.com/ropherpanama/spring-boot-actuator) para que puedas probarlo. 