
## DESCRIPCION
- RED, RED, RED, RED Download the image: [red.png](https://challenge-files.cylabacademy.net/library/fefcf06050d98347e1585e5cb9f2940967f82e0b89c591966473c752de9f3aba/red.png)

## SOLUCION
- Se analizó el título y la descripción del reto, que hacían un énfasis repetitivo en la palabra "RED". Esto fue un indicador directo de que la esteganografía se aplicó aislando exclusivamente el canal de color rojo (Red channel) dentro del modelo de color RGB de la imagen.
    
- Se descargó el archivo `red.png` en el entorno de trabajo de Kali Linux.
    
- Se ejecutó la herramienta especializada de análisis de canales `zsteg` mediante el comando `zsteg red.png`.
    
- La herramienta escaneó y aisló las combinaciones de canales y bits. Al inspeccionar los resultados (específicamente la salida del canal rojo o `b1,r,lsb`), se identificó una cadena de texto sin sentido aparente. Por la estructura de la cadena extraída, se dedujo que el mensaje estaba ofuscado usando codificación Base64.
    
- Se copió la cadena obtenida y se procedió a decodificarla manualmente utilizando la herramienta nativa de la terminal con el comando: `echo "CADENA_BASE64" | base64 -d`.
    
- La decodificación exitosa reveló el mensaje oculto, entregando la bandera del desafío.
- academy{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}

## NOTAS ADICIONALES
- Esteganografía en Canales de Color Individuales: En la composición de imágenes digitales, el modelo RGB establece que cada píxel se forma mezclando Rojo, Verde y Azul. Las técnicas de esteganografía LSB (Least Significant Bit) pueden aplicarse a todos los canales al mismo tiempo, o bien, para dificultar la extracción, enfocarse en modificar los bits de un solo canal de color específico. En este caso, el autor alteró únicamente el color rojo. Herramientas como `zsteg` son esenciales para automatizar la separación de estas capas y buscar firmas o cadenas de texto incrustadas en permutaciones individuales de canales.
## REFERENCIAS
- Reto original: picoCTF 2025 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Esteganografía en canal de color (Red Channel), Manipulación LSB, Herramienta `zsteg`, Codificación Base64.