

## DESCRIPCION
- Files can always be changed in a secret way. Can you find the flag? [cat.jpg](https://challenge-files.cylabacademy.net/library/c585b4adbdaa06f409db7bf5012c2e58e9aab24669764a5f1cf0f9ce0d60dcfd/cat.jpg)

## SOLUCION
```


- Se analizó el título del reto ("information") y el archivo proporcionado (`cat.jpg`), determinando que la técnica requerida involucraba el análisis de la información oculta (metadatos) dentro de la imagen.
    
- En la terminal de Kali Linux, se utilizó la herramienta `exiftool` (un estándar en análisis forense digital) para extraer y leer los metadatos del archivo ejecutando el comando `exiftool cat.jpg`.
    
- Al revisar los atributos arrojados por la herramienta, se identificó una anomalía en el campo `License`, el cual contenía una cadena de texto ofuscada que claramente correspondía a una codificación en formato Base64: `YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9`.
    
- Se identificó una trampa visual generada por el salto de línea automático de la terminal, el cual había empujado el último dígito (`9`) hacia la siguiente línea. Se copió la cadena completa de 44 caracteres y se procesó mediante el decodificador nativo ejecutando `echo "YWNhZGVteXt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9" | base64 -d`.
    
- La decodificación arrojó una salida con formato exacto, revelando la bandera: `academy{the_m3tadata_1s_modified}`.
```

## NOTAS ADICIONALES
- Metadatos y Esteganografía Simple: En el análisis forense (Forensics), los archivos digitales son más que la simple información que muestran en pantalla. Herramientas de edición, sistemas operativos y cámaras incrustan "datos sobre los datos" (metadatos EXIF, IPTC, XMP) directamente en el código del archivo para identificar autores, geolocalización o fechas. Este reto demuestra cómo los campos de texto arbitrarios en los metadatos (como el campo de licencia o copyright) pueden ser explotados como una técnica rudimentaria de esteganografía para infiltrar información secreta, disfrazándola de datos operativos normales.

## REFERENCIAS
- Reto original: picoCTF 2021 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Extracción de Metadatos, Herramienta Exiftool, Codificación Base64, Análisis Forense de Imágenes, Esteganografía Básica.