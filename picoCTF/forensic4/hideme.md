
## DESCRIPCION
- Every file gets a flag. The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here](https://challenge-files.cylabacademy.net/library/67c9b3d090b9350d803c4307cde67459f2c34f853bcd8bf859c5ed1d9b3f0e74/flag.png).

## SOLUCION
```

- Se analizó la etiqueta `steganography` y la descripción del reto, lo que sugirió fuertemente que la imagen proporcionada contenía uno o más archivos adicionales incrustados dentro de su estructura de datos.
    
- Se descargó el archivo de imagen en el entorno de Kali Linux.
    
- Se utilizó la herramienta de análisis forense `binwalk` para escanear el archivo en busca de firmas (magic numbers) correspondientes a otros formatos de archivo conocidos.
    
- Al ejecutar el comando `binwalk flag.png`, el análisis reveló la existencia de un archivo comprimido en formato ZIP incrustado en el desplazamiento hexadecimal `0x3E39` de la imagen original. Los metadatos del ZIP indicaban la presencia de un directorio llamado `secret/` y un archivo interno llamado `flag.png`.
    
- Se procedió a la extracción automatizada del contenido oculto ejecutando el comando `binwalk -e flag.png`.
    
- La herramienta generó un directorio de volcado (`_flag.png.extracted`). Se navegó a la subcarpeta `secret/` y se visualizó la imagen extraída, la cual contenía la bandera renderizada gráficamente en el centro de la imagen.
  
academy{Hiddinng_An_imag3_within_@n_ima9e825f5c50}
```

## NOTAS ADICIONALES
- Incrustación de Archivos y Binwalk: La especificación de muchos formatos de archivo (como JPEG y PNG) indica que el software debe dejar de procesar los datos una vez que encuentra la marca de "fin de archivo" (EOF). Esto permite a los atacantes anexar otros archivos completos, como contenedores ZIP o ejecutables maliciosos, justo después de esta marca. El sistema operativo abrirá la imagen normalmente sin detectar la anomalía. Herramientas como `binwalk` son fundamentales para el Blue Team, ya que ignoran las estructuras lógicas e inspeccionan el archivo byte por byte buscando las firmas hexadecimales características de todo tipo de archivos.

## REFERENCIAS
- Reto original: picoCTF 2023 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Esteganografía por Anexión, Análisis de Firmas de Archivos, Herramienta Binwalk, Extracción de Datos Ocultos.