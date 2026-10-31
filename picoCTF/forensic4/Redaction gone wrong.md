

## DESCRIPCION
- Now you DON’T see me. This [report](https://challenge-files.cylabacademy.net/library/455e6e9581a9272cf0cd6a8f2da0a7cdcfefdb52dc7a7f9c09a27705e2c94103/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?

## SOLUCION
```

- Se analizó la premisa del reto, la cual sugería que un documento contenía un error en el proceso de censura (redaction) de datos sensibles.
    
- Se descargó el documento proporcionado en el enlace **report** y se abrió utilizando un visor de archivos PDF estándar.
    
- Al inspeccionar el documento, se localizaron varios bloques de color negro diseñados para ocultar información crítica a la vista.
    
- Se utilizó el cursor del ratón para sombrear y seleccionar el área sobre los bloques negros, de la misma manera que se selecciona texto normal en cualquier documento.
    
- Se copió el contenido seleccionado y se pegó en un editor de texto plano, lo que reveló que los caracteres seguían intactos por debajo del rectángulo negro.
    
- El texto extraído contenía la llave importante, revelando la bandera: _(Nota: Inserta aquí la bandera exacta que obtuviste al pegar el texto)._
  
  academy{C4n_Y0u_S33_m3_fully}
```

## NOTAS ADICIONALES
- Falsa Censura en PDFs: Este reto explora una vulnerabilidad operativa que ocurre con frecuencia en el mundo corporativo y gubernamental. Al intentar censurar documentos, muchos usuarios simplemente dibujan rectángulos negros o cambian el color de resaltado a negro. Debido a que el formato PDF funciona a través de un sistema de capas superpuestas, esta acción solo añade una capa gráfica superior, pero no elimina la capa de texto vectorial que yace debajo. Cualquier persona puede extraer la información simplemente seleccionando, copiando o utilizando herramientas de terminal como `pdftotext`. Para una censura segura, se deben usar herramientas de sanitización y redacción que eliminen estructuralmente el texto del código fuente del documento.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Análisis de capas en archivos PDF, Extracción de texto oculto, Sanitización y falsa redacción de documentos.