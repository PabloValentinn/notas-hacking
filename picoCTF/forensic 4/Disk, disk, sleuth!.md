
## DESCRIPCION

- Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image. [dds1-alpine.flag.img.gz](https://challenge-files.cylabacademy.net/library/34106bdd624e0aec8af0ba0e9c52e7fd45d5d1415761ffc98b2130cace440057/dds1-alpine.flag.img.gz)

## SOLUCION
```

- Se descargó el archivo comprimido proporcionado por el reto, denominado `dds1-alpine.flag.img.gz`.
    
- Se procedió a descomprimir el archivo utilizando el comando `gunzip dds1-alpine.flag.img.gz` en la terminal de Kali Linux, lo que dio como resultado la imagen de disco en bruto `dds1-alpine.flag.img`.
    
- Siguiendo las instrucciones de la descripción, se utilizó la herramienta `srch_strings`, la cual forma parte de la suite forense _The Sleuth Kit_. Esta herramienta funciona de manera similar al comando estándar `strings` de Linux, extrayendo secuencias de caracteres imprimibles (texto legible) de archivos binarios, pero está optimizada para imágenes de disco.
    
- Para agilizar la búsqueda y aplicar el "terminal-fu" sugerido, se combinó la salida de `srch_strings` con el comando `grep` mediante una tubería (_pipe_), con el objetivo de filtrar únicamente las líneas que contuvieran el formato conocido de la bandera.
    
- Se ejecutó el comando combinado: `srch_strings dds1-alpine.flag.img | grep picoCTF`.
    
- La terminal procesó la imagen de disco e imprimió exitosamente en pantalla la cadena que contenía la bandera, extrayéndola directamente de los datos crudos del disco sin necesidad de montarlo.

 academy{f0r3ns1c4t0r_n30phyt3_6502313d}
```

## NOTAS ADICIONALES
-  Análisis Estático de Imágenes de Disco y Extracción de Cadenas: El análisis de _strings_ es un paso fundamental y preliminar en el análisis forense digital. Extraer cadenas de texto legibles de una imagen de disco cruda (raw image) permite a los investigadores encontrar contraseñas, URLs, direcciones IP, mensajes y, en este caso, banderas de CTF. La ventaja de usar `srch_strings` sobre una imagen no montada es que escanea el disco a nivel de bloques de bytes, lo que significa que recuperará texto incluso si este se encuentra en archivos eliminados, espacio no asignado (slack space) o sectores dañados, los cuales serían invisibles al navegar por el sistema de archivos tradicional.

## REFERENCIAS
 - Reto original: picoCTF 2021 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Disk Image Analysis, String Extraction, The Sleuth Kit (`srch_strings`), Command Line Piping (`grep`).