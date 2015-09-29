---
layout: post
title: "Java : crear un PDF con iText"
date: 2015-09-27 19:35:05 -0500
comments: true
categories: [java, pdf] 
---
>Atención: Este proyecto puedes realizarlo con Eclipse, Netbeans, etc.

En un par de pasos vamos a crear un archivo PDF en JAVA

Materiales:

*    Libreria iText (http://sourceforge.net/projects/itext/files/iText/iText5.2.0/) Para este ejemplo usé la version 5.2.0 (seguro que ya hay una más nueva)
*    Una pequeña imagen: Para este ejemplo usé una imagen en formato PNG, puede ser cualquiera.

Deberás añadir las librerías de iText a tu proyecto (prueba con [Maven](https://maven.apache.org/)), para que puedas hacer uso de las clases que se detallan aquí.

<!--more-->

Teniendo todo esto vamos a crear nuestro archivo.

Vamos a crear una clase con cualquier nombre, en mi caso yo le pondré `CreatePDF` y dentro de ella voy a crear un método llamado `writePDF`. También vamos
a colocarle un método main; el esqueleto quedaria así.

    public class CreatePDF {
        public void writePDF() {...}
        
        public static void main(String args[]) {
            new CreatePDF().writePDF();
        }
    }
	
Luego de esto lo primero que debemos hacer es importar los Objetos que vamos a utilizar, para nuestro básico ejemplo sólo debemos añadir los siguientes:

    import com.itextpdf.text.BaseColor;
    import com.itextpdf.text.Chunk;
    import com.itextpdf.text.Document;
    import com.itextpdf.text.Font;
    import com.itextpdf.text.FontFactory;
    import com.itextpdf.text.Image;
    import com.itextpdf.text.PageSize;
    import com.itextpdf.text.Paragraph;
    import com.itextpdf.text.pdf.PdfWriter;
   
    public class CreatePDF ...
	
Ahora bien, dentro del método `writePDF()` irá toda nuestra lógica para crear nuestro documento, vamos primero a crear un bloque `try/catch` y dentro de él colocaremos las siguientes líneas; las cuales iré explicando paso a paso.

    Document document = new Document(PageSize.LETTER, 80, 80, 50, 50);
    FileOutputStream salida = new FileOutputStream("archivo.pdf");
    PdfWriter writer = PdfWriter.getInstance(document, salida);
    writer.setInitialLeading(0);
	
Como todo en Java debemos tener una instancia de un objeto antes de trabajar con el, por eso debemos tener una referencia a un objeto de tipo
`Document` que es quien representa nuestra hoja en blanco para escribir. Con el atributo `PageSize.LETTER` lo que le estamos indicando es que el
documento tendrá las dimesiones de un archivo en formato CARTA (sí, tambien hay para los demás estandares, investígalos), acompañando lo antes mencionado
está el valor de los márgenes de nuestro documento `(margenIzq, margenDer, margenArriba, margenAbajo)`, pueden ser los valores que gustes compañero.
Con la línea del `FileOutputStream` únicamente estamos creando físicamente nuestro archivo en disco, allí irán todos nuestros cambios al documento.
Luego necesitamos tener una instancia de quien escribirá nuestros cambios y darle su punto de inicio para que pueda escribir, `writer.setInitialLeading(0);`.

Hecho todo esto solo nos queda ir "escribiendo" dentro de nuestro papel en blanco que ya hemos preparado, vamos a añadir dos párrafos sencillos juntos a una imagen.

     Paragraph paragraph = new Paragraph();
     paragraph.add("Primera linea del documento");
     paragraph.setAlignment(Paragraph.ALIGN_CENTER);

Para escribir texto usamos la clase `Paragraph`, como ves tiene un método `add` en el que puedes escribir lo que desees...esta clase tiene muchos métodos interesantes, como el que vemos aquí `paragraph.setAlignment(Paragraph.ALIGN_CENTER)` que como lo
adivinaste es para alinear en donde queramos.

     Image image = Image.getInstance("imagen.png");
     image.scaleToFit(150, 150);
     image.setAlignment(Chunk.ALIGN_CENTER);

Para colocar imégenes debemos instanciar un objeto de tipo `Image`, darle la ubicación de nuestra imagen al constructor, darle el tamaño que gustemos y alinearla.

     Paragraph paragraph_2 = new Paragraph();
     paragraph_2.setFont(new Font(FontFactory.getFont("Courier", 12, Font.BOLD, BaseColor.ORANGE)));
     paragraph_2.add("Ultima linea del documento");
     paragraph_2.setAlignment(Paragraph.ALIGN_LEFT);
	 
En este parrafo lo único que hemos hecho diferente es darle una fuente y color especifico a nuestro texto, hay otras formas de hacerlo
incluso si tienes fuentes extrañas instaladas en su carpeta Fonts de Windows puedes crear una nueva fuente a partir de esa, ya que por lo
general las fuentes "extrañas" no las reconoce, hagan la prueba y me comentan (si si si, tengo la solución si les llega a pasar..)

Antes de añadir todo nuestro contenido debemos abrir el documento para poder usarlo `document.open();` luego ir añadiendo en el orden en que queremos que aparezcan todos los checheres que hemos creado

    document.add(paragraph);
    document.add(image);
    document.add(paragraph_2);

y por lógica... si abres algo, ciérralo. `document.close();`

Eso es todo! Luego de que lo ejecutes deberás tener en tu carpeta de proyecto tu archivo PDF.
Saludos, para dudas a la orden!!! 
