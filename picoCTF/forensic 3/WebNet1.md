
## DESCRIPCION

- We found this [packet capture](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/webnet1-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/afb7599dd63cad30a04eb98d0e4057608120371eb3e8943b632505e32c8b622c/picopico.key). Recover the flag.

## SOLUCION
```

- Se descargaron los archivos correspondientes a la captura de red (`packet capture`) y la llave criptográfica (`key`) proporcionados en la plataforma del reto.
    
- Se abrió el archivo de captura en la herramienta Wireshark. Al observar que el tráfico web estaba cifrado mediante el protocolo TLS, se procedió a vulnerar esta capa de seguridad de la misma forma que en el reto anterior.
    
- Se cargó la llave privada (`key`) en las configuraciones de Wireshark (`Edit` -> `Preferences` -> `Protocols` -> `TLS` -> "RSA keys list") para habilitar el descifrado pasivo del tráfico interceptado.
    
- Una vez que los paquetes HTTP fueron descifrados y revelados en texto claro, se inspeccionó el flujo de datos y se identificó la descarga de un archivo de imagen desde el servidor.
    
- Se utilizó la funcionalidad de extracción de Wireshark (`File` -> `Export Objects` -> `HTTP`) para guardar la imagen transmitida localmente en el equipo.
    
- Posteriormente, se ejecutó la herramienta de línea de comandos `exiftool` sobre la imagen extraída para analizar a profundidad todos sus metadatos.
    
- Al revisar la salida de `exiftool`, se localizó la bandera del reto, la cual había sido inyectada intencionalmente dentro de uno de los campos de texto de los metadatos de la imagen.
  
  academy{honey.roasted.peanuts}

```

## NOTAS ADICIONALES
- Extracción de Objetos de Red y Análisis de Metadatos: Este escenario requiere combinar técnicas de análisis de tráfico con análisis forense de archivos. Tras romper la capa de cifrado de transporte (TLS), un auditor puede reconstruir los flujos TCP y extraer los archivos binarios exactos que viajaron por la red. Herramientas como `exiftool` son fundamentales en la etapa posterior, ya que permiten leer atributos ocultos (datos EXIF, IPTC, perfiles de color o comentarios) donde actores maliciosos o creadores de retos suelen ocultar cargas útiles (payloads), firmas o información confidencial que no es visible al abrir la imagen en un visor convencional.

## REFERENCIAS
- - Reto original: picoCTF 2019 - Categoría: Forensics (WebNet1).
    
- Conceptos aplicados: TLS/SSL Decryption, Network Object Extraction, Metadata Analysis, Wireshark, ExifTool.
