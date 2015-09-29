---
layout: post
title: "Apuntes - Tuning Glassfish (Optimización para producción)"
date: 2015-09-29 11:20:00 -0500
comments: true
categories: javaee glassfish oracle
---

###Ajuste de JVM 

Ya que Glassfish está hecho sobre Java, muchas de las optimizaciones pueden hacerse a través de la Java Virtual Machine

En el fichero `domain.xml` ubicado en `%GLASSFISH_HOME%/glassfish/domains/<DOMAIN_NAME/config` se deben editar los parametro `Xms` y `Xmx`, esto para reservar más memoria para el GF. 

Ubica los siguientes parámetros y modifícalos según la necesidad y capacidad del servervidor que aloja tu aplicación: 

`<jvm-options>-Xmx1024m</jvm-options>` y `<jvm-options>-Xms1024m</jvm-options>`

En este caso se está asignando 1GB de RAM, ambos parámetros se colocan igual para asignar la memoria en el arranque del servicio, de esta forma no se pierde tiempo haciéndolo después.

Modificar la opción `-client` por `-server` de la siguiente manera, si el servidor que ejecuta el GF es 64bits entonces por default tomará la opción correcta, pero nada se pierde con “asegurarnos":`<jvm-options>-server</jvm-options>`

También incluir estas configuraciones `-Xss128k`, `-XX:+DisableExplicitGC`, `-XX:ParallelGCThreads=N` (en donde N es el número de CPU's del servidor si la cantidad es menor a 8, en caso contrario N es igual #CPU's/2)

`-XX:+UseParallelOldGC`

Si la aplicación está haciendo una gran cantidad de operaciones de E/S como escritura, también se le puede decir a `Grizzly` que utilice una estrategia asíncrona:

`-Dcom.sun.grizzly.http.asyncwrite.enabled=true`

Una alternativa que podría considerarse también si se está notando que algunas operaciones de escritura parecen tomar más tiempo de lo esperado.  Se puede aumentar el número de procesadores de escritura al aumentar el número Selectors NIO:

`-Dcom.sun.grizzly.maxSelectors=XXX`

Si la aplicación será utilizada por dispostivos móviles o a través de redes lentas puede configurar: 

`-Dcom.sun.grizzly.readTimeout`
o 
`network-config>network-listeners>network-listener>transport#read-timeout` para las operaciones read y `com.sun.grizzly.writeTimeout o network-config>network-listeners>network-listener>transport#write-timeout` para las operaciones write. 

Para que un hilo no bloquee otros posibles procesos de I/O durante mucho tiempo puede configurar la opción:

`-Dcom.sun.grizzly.useKeepAliveAlgorithm=true`

Esto le dará oportunidad de ejecución a otras peticiones.

### GlassFish Tuning

Algunas configuraciones en el servidor de aplicaciones en sí, pueden ser las siguientes:

En el mismo fichero `domain.xml` modificar las siguientes opciones como se muestra a continuación:

1. Evitemos el autodeploy y la recarga dinámica, esto toma tiempo y no es deseable, configuramos lo siguiente: `<das-config autodeploy-enabled="false" dynamic-reload-enabled="false"></das-config>`
2. Aceptor Threads: Si se tiene por ejemplo, un servidor con 2 CPU's de 4 núcleos cada uno, el valor de este parámetro debe ser 8. Para configurarlo ve a la consola de administración y busca la siguiente direccion `Configuration -> Network Config -> Transports -> tcp -> Acceptor threads`
3. Cacheo de recursos estáticos: `Configuration -> Network Config -> Protocols -> http-listener-1 -> File Cache -> Enabled`. De tener conexiones HTTPS habilitarlo también para el listener seguro.
4. Si el servidor solo posee un Network Interface Card (NIC) reemplaza todos los valores `0.0.0.0` de  los http listeners con el IP del servidor, como se muestra `Configuration -> Network Config -> Network Listeners -> <listener_name> -> Address`
5. Modificar el fichero `default-web.xml` ubicado en `%GLASSFISH_HOME%/glassfish/domains/<DOMAIN_NAME>/config` como se muestra:  

        <servlet>
	    <servlet-name>jsp</servlet-name>
        <servlet-class>org.apache.jasper.servlet.JspServlet</servlet-class>
            <init-param>
                <param-name>development</param-name>
                <param-value>false</param-value>
            </init-param>
            <init-param>
                <param-name>genStrAsCharArray</param-name>
                <param-value>true</param-value>
            </init-param>
            ...
        </servlet>

### Optimizaciones para JDBC

Para drivers JDBC de Oracle pueden configurarse las siguientes opciones:

* `ImplicitCachingEnabled=true`
* `MaxStatements=200`
* Configurar los valores del Pool de conexiones `steady-pool-size` y `max-pool-size` con el mismo valor. Una regla general es configurar estos valores con el mismo número que se ha configurado en los `HTTP request processing threads`

Sobre la marcha seguimos trabajando con Glassfish (ahora en su versión 4) y estos ajustes seguro que se irán actualizando.

A todos un saludo!