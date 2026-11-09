
## DESCRIPCION
- You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag. Download the jpg image [here](https://challenge-files.cylabacademy.net/library/364c5c391edaf4ab3da852e0fc51a5285bc4a570900618b112c52805fc1d5c14/img.jpg).

## SOLUCION
```

- Se descargó la imagen provista (`img.jpg`).
    
- **Análisis de Metadatos (`exiftool`):**
    
    - Se examinaron los campos EXIF de la imagen, encontrando una cadena sospechosa codificada en Base64 dentro del comentario (`Comment: c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9`).
        
- **Decodificación:**
    
    - Al decodificar el comentario, se reveló el uso de la herramienta `steghide` junto con una contraseña en Base64 (`cEF6endvcmQ=` $\rightarrow$ `pAzzword`).
        
- **Extracción Esteganográfica:**
    
    - Se extrajo el contenido oculto mediante `steghide extract -sf img.jpg -p "pAzzword"` para recuperar el archivo de texto con la bandera.
```

## NOTAS ADICIONALES
- **Esteganografía en Imágenes:** Herramientas como `steghide` permiten ocultar información de manera imperceptible dentro de los bits menos significativos (LSB) de una imagen JPG o BMP, requiriendo metadatos, comentarios o contraseñas incrustadas para su posterior extracción.

## REFERENCIAS
- Reto original: picoMini by CMU-Africa - Categoría: Forensics (Easy).
    
- Autor: Yahaya Meddy.