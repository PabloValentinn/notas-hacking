

## DESCRIPCION
- I found this cipher in an old book.

## SOLUCION
```


- Se desplegó la instancia del desafío y se capturó el texto cifrado conectándose al servidor remoto desde la terminal de Kali Linux mediante el comando `nc xebec.cylabacademy.net 31291`.
    
- El servidor devolvió un texto extenso (comenzando con "Ne iy nytkwpsznyg..."). Al carecer de la llave, se determinó que la vía de solución debía ser el criptoanálisis.
    
- Debido a la considerable longitud del mensaje, se sometió el texto a un análisis estadístico de frecuencia de caracteres utilizando herramientas automatizadas para romper algoritmos polialfabéticos.
    
- El criptoanálisis reveló rápidamente que la llave estática utilizada era la palabra `flag`.
    
- Al aplicar la llave `flag` al criptograma, se obtuvo un texto completamente legible en inglés sobre los orígenes históricos del cifrado, el cual contenía la bandera expuesta en su último párrafo: `academy{b311a50_0r_v1gn3r3_c1ph3r181ba1aa}`.
  
  
```

## NOTAS ADICIONALES
- Vulnerabilidad del Cifrado de Vigenère: Aunque históricamente fue conocido como "el cifrado indescifrable" (_le chiffre indéchiffrable_), este reto demuestra su principal debilidad empírica. Cuando se utiliza una llave corta que se repite en bucle sobre un texto suficientemente largo, los patrones estadísticos del idioma original (las letras y palabras más comunes del inglés) inevitablemente "atraviesan" la capa de encriptación. Técnicas matemáticas como el Examen de Kasiski o el Índice de Coincidencia explotan estas repeticiones para deducir la longitud exacta de la llave y, posteriormente, descifrar los caracteres mediante puro análisis de frecuencia, permitiendo romper la seguridad de forma analítica sin necesidad de fuerza bruta ciega.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Cifrado de Vigenère, Análisis de Frecuencias, Método Kasiski, Criptoanálisis.
