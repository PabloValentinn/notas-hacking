
## DESCRIPCION
- Download this image and find the flag.

- [Download image](https://challenge-files.cylabacademy.net/library/8087998f70644cca47cf39fce5707a2b62b6d91d28f345ecc874238626c1cad2/academy.flag.png)

## SOLUCION
```

- Se analizó el título del desafío ("St3g0") y la etiqueta proporcionada (`steganography`), lo que indicó que el archivo PNG contenía información oculta directamente en la estructura de sus píxeles.
    
- Se descargó la imagen al entorno de trabajo en Kali Linux bajo el nombre `academy.flag.png`.
    
- Se procedió a instalar la herramienta especializada en esteganografía `zsteg` utilizando el gestor de paquetes de Ruby mediante el comando `sudo gem install zsteg`.
    
- Una vez instalada, se ejecutó el análisis automatizado contra la imagen con el comando `zsteg academy.flag.png`.
    
- La herramienta escaneó los canales de color (Rojo, Verde, Azul) y extrajo el texto oculto en los bits menos significativos (LSB), arrojando la bandera en texto claro en la terminal. _(Nota: Inserta aquí la bandera exacta que te devolvió el comando, usualmente con el formato `academy{...}` o `picoCTF{...}`)._
  
  academy{7h3r3_15_n0_5p00n_3e86461e}
```

## NOTAS ADICIONALES
- Esteganografía LSB (Least Significant Bit): A diferencia de los metadatos que actúan como "etiquetas" del archivo, la técnica LSB altera directamente los datos visuales de la imagen. Modifica el último bit (el menos significativo) del valor de cada color en un píxel. Al ser el cambio tan minúsculo (por ejemplo, cambiar un valor de rojo de 255 a 254), el ojo humano es incapaz de percibir la diferencia en la imagen resultante. Herramientas como `zsteg` son fundamentales en el análisis forense porque automatizan la extracción de estas secuencias de bits alterados en archivos de formato sin pérdida (lossless) como PNG y BMP.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Esteganografía, Manipulación LSB (Bit Menos Significativo), Análisis Forense de Imágenes, Herramienta `zsteg`.