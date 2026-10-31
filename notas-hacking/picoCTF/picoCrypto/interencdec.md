
## DESCRIPCION

- Can you get the real meaning from this file.

Download the file [here](https://challenge-files.cylabacademy.net/library/da8169e4d440c1f815ceb129ecb79e4da3bb5027d7807fa9e3e9fb1e124d99fb/enc_flag).

## SOLUCION
```
- Se analizó el título del reto ("interencdec") y las etiquetas proporcionadas (`base64`, `caesar`), las cuales sugerían que la bandera estaba ofuscada bajo múltiples capas de codificación y cifrado.
    
- Se descargó el archivo `enc_flag` y se visualizó su contenido en la terminal, revelando una cadena codificada en Base64.
    
- Se aplicó una primera pasada de decodificación mediante el comando `base64 -d`, lo que arrojó una segunda cadena de texto en formato de bytes (comenzando con `b'...'`) que también estaba codificada en Base64.
    
- Se extrajo y decodificó esta segunda capa de Base64, revelando el texto `hjhkltf{jhlzhy_k3jy9wa3k_96j73745}`.
    
- Reconociendo la estructura típica de una bandera pero con los caracteres alterados, se procedió a aplicar un criptoanálisis de Cifrado César.
    
- Se determinó que al aplicar un desplazamiento de -7 (o ROT19) a los caracteres alfabéticos, el texto revelaba la envoltura oficial de la plataforma y el mensaje en claro, obteniendo la bandera: `academy{caesar_d3cr9pt3d_96c73745}`.


```

## NOTAS ADICIONALES
- Ofuscación por Capas (Onion Encoding): Este reto es un excelente ejemplo introductorio a la técnica de anidar múltiples métodos de ofuscación ("pelar la cebolla"). Combina la codificación de datos binarios a texto (Base64, diseñado para el transporte seguro de datos, no para ocultarlos) con criptografía clásica de sustitución (Cifrado César). En la práctica real, los analistas de malware y equipos de respuesta a incidentes a menudo encuentran código malicioso (payloads) ofuscado bajo múltiples capas de Base64, HEX, y operaciones matemáticas simples (como XOR o ROT) diseñadas para evadir los sistemas de detección de antivirus basados en firmas.

## REFERENCIAS
- Reto original: picoCTF 2024 - Categoría: Cryptography (Easy).
    
- Conceptos aplicados: Codificación Base64, Cifrado César, Ofuscación por capas, Manipulación de datos en CLI de Linux.
