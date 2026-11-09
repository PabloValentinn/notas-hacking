

## DESCRIPCION
- We found this file. Recover the flag. [tunn3l_v1s10n](https://challenge-files.cylabacademy.net/library/3b5add918cb4cf98fa62ef4e05eb8c55c6c9ae547a939c6be992ee3aa656ee69/tunn3l_v1s10n)
## SOLUCION
``` 

- Se descargó el archivo objetivo `tunn3l_v1s10n`, el cual carecía de extensión.
    
- Mediante análisis de firmas ("Magic Bytes"), se identificó que los dos primeros bytes del archivo (`42 4D`) correspondían a la firma de un archivo de imagen en formato BMP.
    
- Al intentar visualizar la imagen, el sistema arrojó un error de formato. Se procedió a utilizar un editor hexadecimal (como `hexeditor`) para inspeccionar la estructura de la cabecera del archivo BMP, identificando valores anómalos (`BA D0`) insertados de forma intencional para corromper la lectura.
    
- Se reparó el archivo sobrescribiendo dos offsets críticos con los valores estándar de la especificación BMP:
    
    - El offset `0x0A` (que indica el inicio del arreglo de píxeles) se ajustó a `36 00 00 00` (54 bytes).
        
    - El offset `0x0E` (que indica el tamaño de la cabecera DIB) se ajustó a `28 00 00 00` (40 bytes).
        
- Tras esta primera reparación, la imagen pudo abrirse, mostrando un paisaje visualmente recortado con el texto señuelo "NOT THE FLAG".
    
- Siguiendo la pista del título del reto ("tunn3l v1s10n" o visión de túnel), se dedujo que los metadatos de dimensiones habían sido alterados para ocultar información.
    
- Se regresó al editor hexadecimal y se localizó el parámetro de altura de la imagen (height) en el offset `0x16`. Se incrementó el valor hexadecimal original de `32 01` a `32 03` para expandir el lienzo de la imagen de forma vertical.
    
- Al renderizar la imagen con la nueva altura, se reveló el área oculta en la parte superior del lienzo.
    
- Debido a que las dimensiones inusuales de la imagen (un ancho de 1134 píxeles) causaban conflictos y recortes en los visores de imágenes nativos de Linux, se procedió a renderizar el archivo a través de un navegador web (Firefox) o utilizando herramientas de redimensionamiento por línea de comandos (`ImageMagick`) para alejar la vista sin corromper el alineamiento de los píxeles, logrando leer y extraer la bandera completa de forma exitosa.
  
  
```

## NOTAS ADICIONALES
- Estructura de Cabeceras BMP y Manipulación Hexadecimal: Este escenario evalúa la comprensión profunda de las especificaciones de formatos de archivo estándar (File Signatures and Header Structures). En un archivo BMP, las ubicaciones de bytes específicas dictan de manera estricta el tamaño del archivo, las dimensiones del lienzo (ancho y alto), la profundidad de color y el punto exacto donde comienzan los datos de la imagen renderizable. Modificar el parámetro de altura permite revelar datos ocultos (esteganografía por alteración de dimensiones) sin modificar la información real de los píxeles, mientras que alterar el parámetro de ancho destruiría el _stride_ (la alineación de las filas de píxeles), corrompiendo visualmente la imagen.
## REFERENCIAS
- - Reto original: picoCTF 2021 - Categoría: Forensics.
    
- Conceptos aplicados: Hex Editing, BMP File Structure, Header Recovery, Metadata Manipulation, Image Carving.