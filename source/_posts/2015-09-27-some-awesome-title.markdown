---
layout: post
title: "Threads Java: iniciarlos, detenerlos y reanudarlos (básico)"
date: 2015-09-27 20:51:29 -0500
comments: true
categories: [java, threads]
---

Bien, primero que nada explicar de que vá el asunto.

La idea es controlar la ejecución de un `Thread`; es decir, poder detenerlo y reanudarlo. De plano que para iniciarlo lo iniciamos en el main y que también podamos detener del todo el proceso (para no poder levantarlo más).
Explico un poco el enfoque de la solución, implementé un `Proceso` principal, este es el trabajo que debe hacer el `Thread`; simplemente consiste en imprimir un número cada cierto tiempo, un tiempo random no mayor a 5 segundos.

<!--more-->

>Decir que esto se ejecutará infinitamente.

####Clase `Proceso.java`

    import java.util.Random;
    
    /**
     * @author ropherpanama@gmail.com
     * Esta clase representa el proceso de trabajo; imprimir un entero cada cierto tiempo
     * se sobrescriben los metodos suspend y resume
     */
    public class Proceso implements Runnable {
        private int currentCont;
        private Thread t;
        private final int sleepTime;
        boolean suspended = false;
        private String threadName;
        private boolean working = true;
        private final static Random generator = new Random();
    
        public Proceso(String threadName) {
            this.threadName = threadName;
            sleepTime = generator.nextInt(5000);
            currentCont = 0;
        }
    
        @Override
        public void run() {
            System.out.println("Running " + threadName);
            try {
                while (isWorking()) {
                    System.out.println(threadName + " doing : " + currentCont);
                    currentCont++;
                    Thread.sleep(sleepTime);
    
                    synchronized (this) {
                        while (suspended) {
                            wait();
                        }
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
        public void start() {
            System.out.println("Starting " + threadName);
            if (t == null) {
                t = new Thread(this, threadName);
                t.start();
            }
        }
    
        void suspend() {
            System.out.println("Suspending " + threadName);
            suspended = true;
        }
    
        synchronized void resume() {
            System.out.println("Resuming " + threadName);
            suspended = false;
            notify();
        }
    
        public boolean isWorking() {
            return working;
        }
    
        public void setWorking(boolean working) {
            this.working = working;
        }
    }

Notar que el propio hilo se sincroniza y si se cumple que el hilo entra en estado `suspend` se llama al método `wait()`, esto provocará que el hilo se mantenga pausado hasta que alguien llame al método `notify();` que precisamente se llama en el método `resume()` y se niega que el estado del hilo es `suspend (suspend = false)`. Otro punto importante es que al tener un proceso que podría ejecutarse hasta el final de los tiempos, podríamos querer algún día detenerlo, para eso usamos el `while` con la variable `working`, que en primera instancia tendra un valor `true`.

###Interactuar por consola con tu Thread

Lo divertido del caso era que se pudiera; mediante el teclado decirle al `Thread` lo que tenía que hacer, no simplemente escribirlo y no poder interactuar con el programa. Para eso, pensé en un "monitor" de entrada de teclado (`Thread` también por cierto) que en base a lo que escribas en el teclado defina el estado del `Thread` que está realizando el proceso principal. Entonces puedo escribir S (suspender), D (detener), R (reanudar) y B (salir) y con esto podré controlar los estados de mi hilo `Proceso`. Para este ejemplo simple solo estoy vigilando un solo `Thread` pero pueden ser cuantos se requieran.

####Clase `Entrada.java`

import java.util.Scanner;

    /**
     * @author ropherpanama@gmail.com
     * Esta clase esta pendiente de la entrada del usuario, la misma actua
     * como monitor de entrada por teclado y dependiendo de ello ajustara el estado
     * del Hilo al cual controla
     *
     */
    public class Entrada implements Runnable {
        private Scanner sc = new Scanner(System.in);
        private String command = "";
        private Proceso p1;
    
        public Entrada(Proceso p1) {
            this.p1 = p1;
        }
    
        @Override
        public void run() {
            while (true) {
                System.out.println("Waiting input:");
                command = sc.nextLine();
    
                if (this.getCommand().toUpperCase().equals("S")) {
                    p1.suspend();
                } else if (this.getCommand().toUpperCase().equals("R")) {
                    p1.resume();
                } else if (this.getCommand().toUpperCase().equals("D")) {
                    p1.setWorking(false);
                    System.out.println("Fin de trabajo");
                } else if (this.getCommand().toUpperCase().equals("B")) {
                    System.out.println("Saliendo");
                    System.exit(0);
                } else
                    System.out.println("No input");
            }
        }
    
        public String getCommand() {
            return command;
        }
    
        public void setCommand(String command) {
            this.command = command;
        }
    }

Vemos que esta clase, al igual que `Proceso` implementa a la clase `Runnable`, por ende tambien es un `Thread`. Este hilo va a estar pendiente de lo que escribas en el teclado y según ello actuará sobre el `Thread` que este monitorizando.

####Vamos a probar!

Ahora vamos a probar esto, creamos la clase `Test.java` que contiene el main y lo ponemos todo a interactuar.

####Clase `Test.java`

    public class Test {
        public static void main(String[] args) {
            Proceso p1 = new Proceso("Juana");
            p1.start();
           
            Entrada e = new Entrada(p1);
            Thread input = new Thread(e);
            input.start();
        }
    }

Bien, he llamado a mi proceso principal "Juana" (no sé porqué) y le he dicho que inicie `(p1.start())`, luego; he creado una instancia de mi `Thread` monitor de entrada, para que vigile lo que escribo y opere sobre "Juana". Notar que le paso a "Juana" (p1) como argumento de su constructor `Entrada e = new Entrada(p1);`
 
La salida del programa es la siguiente:

    Starting Juana
    Running Juana
    Juana doing : 0
    Waiting input:
    Juana doing : 1
    Juana doing : 2
    Juana doing : 3
    Juana doing : 4
    Juana doing : 5
    Juana doing : 6
    Juana doing : 7
    Juana doing : 8
    S
    Juana doing : 9
    
    Suspending Juana
    Waiting input:
    R
    Resuming Juana
    Waiting input:
    Juana doing : 10
    Juana doing : 11
    Juana doing : 12
    Juana doing : 13
    Juana doing : 14
    Juana doing : 15
    Juana doing : 16
    B
    Juana doing : 17
    
    Saliendo

Juana inicio y se ejecutó, e inició a tirar sus números. Luego le dije Juana descanza un rato (S) y descanzó hasta que le dije continúa (R), siguió hasta el número 17 y le dije sal del programa totalmente (B)

Si te quedan dudas te invito a ver la video demostración en Youtube, pronto pongo el link.

Saludos! 
