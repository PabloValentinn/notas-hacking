

## DESCRIPCION
- How about some hide and seek?

Download this file [here](https://challenge-files.cylabacademy.net/library/26d33b97d1745fc99c1cf94e3783a3dc963b8b667ca6960ebfce48aa9909251c/unknown.zip).

## SOLUCION
```

- Se analizó la pista proporcionada, la cual sugería revisar la "información sobre la imagen", haciendo referencia directa a la extracción y análisis de metadatos.
    
- Se descargó el archivo comprimido `unknown.zip` en el entorno de trabajo de Kali Linux.
    
- Inicialmente se ejecutó un análisis sobre el archivo ZIP, pero al identificar que los metadatos pertenecían al contenedor y no a la imagen, se procedió a descomprimir el archivo ejecutando `unzip unknown.zip`. Esto extrajo la imagen real denominada `ukn_reality.jpg`.
    
- Se aplicó la herramienta de análisis forense digital a la imagen ejecutando el comando `exiftool ukn_reality.jpg`.
    
- Al revisar detalladamente la lista de atributos arrojados por la herramienta, se identificó una anomalía en uno de los campos de texto libre, el cual contenía una cadena ofuscada que correspondía a una codificación en formato Base64: _(Nota: Inserta aquí la cadena Base64 que encontraste)_.
    
- Se copió la cadena sospechosa y se procesó mediante el decodificador nativo de la terminal utilizando el comando `echo "CADENA_BASE64" | base64 -d`.
    
- La decodificación exitosa reveló el texto oculto en claro, entregando la bandera
  
  academy{ME74D47A_HIDD3N_aebe8c0f}

```

## NOTAS ADICIONALES
- Metadatos y Archivos Anidados: Este desafío refuerza los conceptos de extracción de metadatos y esteganografía básica vistos en retos anteriores, pero añade una capa administrativa que es muy común en el trabajo forense real: la recolección de evidencia empaquetada. Demuestra la importancia de identificar y preparar correctamente la evidencia (extrayendo los archivos de sus contenedores `.zip`, `.tar` o `.gz`) antes de aplicar herramientas de análisis profundo. Aplicar una herramienta forense al "sobre" (el ZIP) no revelará los secretos de la "carta" (la imagen).
## REFERENCIAS
- Reto original: picoCTF 2024 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Extracción de Metadatos, Herramienta `exiftool`, Codificación Base64, Análisis de Archivos Anidados.