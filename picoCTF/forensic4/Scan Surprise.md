
## DESCRIPCION
- I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?

You can download the challenge files here:

- [challenge.zip](https://challenge-files.cylabacademy.net/library/55c0e897129786cdc2c3f7c8f08e346866d9c187f20adf8b2f22a0ed2fe76e37/challenge.zip)

## SOLUCION
```

- Se analizó la descripción del reto y sus etiquetas, específicamente la etiqueta `qr_code`, lo que indicó que la información oculta no requería extracción de metadatos ni manipulación de bits, sino la decodificación de una imagen estandarizada de Código QR.
    
- Se descargó el archivo comprimido `challenge.zip` al entorno local.
    
- Se procedió a descomprimir el archivo, obteniendo como resultado un directorio que contenía una imagen (típicamente `flag.png`).
    
- Al abrir la imagen con un visor gráfico estándar, se visualizó en pantalla un Código QR (Quick Response code).
    
- Utilizando la cámara y el software lector de códigos integrado en un dispositivo móvil (Opción 1), se escaneó directamente la pantalla del monitor.
    
- El dispositivo móvil decodificó exitosamente el patrón bidimensional del QR, revelando el texto plano contenido en él.
  
  academy{p33k_@_b00_5f0d36e7}
```

## NOTAS ADICIONALES
- Códigos QR en CTFs: Los Códigos de Respuesta Rápida (QR) son una forma de codificación óptica bidimensional inventada originalmente para la industria automotriz. En el contexto de la ciberseguridad y los CTFs (categoría Forensics o Misc), representan la forma más básica de ofuscación de datos a simple vista. A diferencia de la esteganografía (donde el secreto está oculto) o la criptografía (donde el secreto está bloqueado por una llave matemática), la información en un QR está expuesta públicamente pero requiere un decodificador visual específico para ser interpretada y convertida a texto legible por humanos.

## REFERENCIAS
- Reto original: picoCTF 2024 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Decodificación Óptica, Códigos QR, Extracción de Datos Gráficos.