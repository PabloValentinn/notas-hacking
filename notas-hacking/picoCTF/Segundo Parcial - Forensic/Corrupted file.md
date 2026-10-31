

## DESCRIPCION
- This file seems broken... or is it? Maybe a couple of bytes could make all the difference. Can you figure out how to bring it back to life? Download the file [here](https://challenge-files.cylabacademy.net/library/03e658f970a580c265471fa9e2477a66457bed10e5f89da0fe70c141c3509f3b/file).

## SOLUCION
```

- Se descargó e inspeccionó el archivo dañado del reto (`file`).
    
- **Análisis de Cabecera (_Magic Bytes_):**
    
    - Se analizó la estructura hexadecimal inicial con `xxd file | head -n 5`.
        
    - Se identificó la estructura interna de una imagen JPEG/JFIF, pero con los dos primeros bytes corruptos (`5c 78` en lugar del marcador estándar SOI: `ff d8`).
        
- **Restauración Binaria:**
    
    - Se corrigió la cabecera reemplazando los bytes iniciales por la firma legítima de inicio de JPEG (`\xff\xd8`):
        
        Bash
        
        ```
        python3 -c "with open('file', 'rb') as f: data = f.read(); open('flag.jpg', 'wb').write(b'\xff\xd8' + data[2:])"
        ```
        
- **Extracción de la Bandera:**
    
    - Al restaurar la estructura del contenedor, el archivo `flag.jpg` quedó legible y se visualizó la bandera directamente dentro de la imagen recuperada.
        
- **Bandera:** Obtenida al abrir y leer el texto renderizado en `flag.jpg`.
```

## NOTAS ADICIONALES
- **Validación de Firmas Binarias:** Los sistemas operativos y visores dependen de los números mágicos (_magic numbers_) ubicados al inicio de los archivos para determinar su formato real, independientemente de la extensión. En imágenes JPEG, la ausencia del marcador de inicio `FF D8` invalida el archivo para cualquier decodificador estándar hasta que se restituye manualmente la cabecera conforme a la especificación JFIF.

## REFERENCIAS
- Reto original: picoMini by CMU-Africa - Categoría: Forensics (Easy).
    
- Autor: Yahaya Meddy.
