
## DESCRIPCION
- The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?

Download the suspicious file [here](https://challenge-files.cylabacademy.net/library/648efad3a02ebcd4c6fa34acb864030945055931c435b53f28821b672500ad3c/flag2of2-final.pdf).

## SOLUCION
```

- Se analizó la descripción del reto y las etiquetas proporcionadas (`file_format`, `polyglot`), determinando que el archivo descargado era un "archivo políglota" (un archivo diseñado maliciosamente o por diversión para ser válido bajo dos o más especificaciones de formato distintas de manera simultánea).
    
- Se descargó el archivo sospechoso en el entorno de Kali Linux.
    
- **Análisis de Identidad 1 (PDF):** Se renombró el archivo agregándole la extensión `.pdf` (ejecutando `mv archivo_descargado archivo.pdf`). Al abrirlo con un visor de documentos, el programa interpretó la estructura vectorial y de texto, revelando en pantalla la segunda mitad de la bandera: `1n_pn9_&_pdf_07226ac4}`. (También se confirmó la extracción de esta capa utilizando `binwalk`, lo que arrojó el código fuente en crudo `7 (1n_pn9_&_pdf_07226ac4})Tj`).
    
- **Análisis de Identidad 2 (PNG):** Se renombró el mismo archivo cambiando su extensión a `.png` (ejecutando `mv archivo.pdf archivo.png`). Debido a que los visores estrictos pueden fallar al encontrar el código PDF subyacente, se forzó el renderizado de la imagen utilizando el motor de un navegador web (ej. `firefox archivo.png`). El navegador ignoró la sintaxis del PDF y leyó los datos de los píxeles incrustados, visualizando en pantalla la primera mitad de la bandera (`picoCTF{...`).
    
- Se concatenaron ambas partes extraídas de las dos identidades del archivo, obteniendo la bandera fina
```

## NOTAS ADICIONALES
- Archivos Políglotas (Polyglots): En ciberseguridad, un archivo políglota explota la tolerancia a fallos y las diferencias de interpretación de distintos programas o sistemas operativos. Dado que muchos formatos no requieren que sus firmas mágicas (magic bytes) o encabezados comiencen exactamente en el byte 0 (o ignoran la "basura" al final del archivo), los atacantes pueden fusionar un ejecutable con un PDF o un script de JavaScript dentro de una imagen. Esto permite evadir filtros de seguridad y sistemas de detección de intrusos (IDS) que podrían clasificar el archivo como inofensivo basándose en una sola de sus múltiples "identidades".

## REFERENCIAS
- Reto original: picoCTF 2024 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Archivos Políglotas, Evasión de Formatos, Análisis de Múltiples Vectores, Motores de Renderizado Gráfico.