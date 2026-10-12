

## DESCRIPCION
- We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with `nc chatelaine.cylabacademy.net 12955`.

## SOLUCION
```


- Se identificó a partir de la descripción ("hicimos un montón de sustituciones") que el desafío empleaba un Cifrado de Sustitución Monoalfabética.
    
- Se capturó el criptograma conectándose al servidor remoto a través de la terminal en Kali Linux utilizando el comando `nc chatelaine.cylabacademy.net 12955`. El servidor devolvió un extenso bloque de texto ofuscado.
    
- Dado que el alfabeto había sido mezclado aleatoriamente (superando la capacidad de un ataque de fuerza bruta simple), se recurrió a una herramienta automatizada de análisis de frecuencias de caracteres (como quipqiup).
    
- La herramienta realizó un análisis estadístico emparejando los símbolos del criptograma con la frecuencia de aparición natural de las letras en el idioma inglés, logrando reconstruir el alfabeto original y traduciendo el mensaje a un texto legible (un fragmento de la novela _Heart of Darkness_).
    
- La primera línea del texto descifrado indicaba explícitamente el contenido de la bandera. Tras verificar las validaciones del servidor, se determinó que la solución debía enviarse como una "bandera cruda" (sin envolturas como `picoCTF{}` o `academy{}`), resultando en el envío exitoso de: `frequency_is_c_over_lambda_lrwpcbmnsy`.
  
```

## NOTAS ADICIONALES
- Sustitución Monoalfabética y Análisis de Frecuencias: Una sustitución monoalfabética aleatoria posee 26! (factorial de 26) posibles claves, lo que la hace inmune a ataques de fuerza bruta básicos. Sin embargo, su principal debilidad es que preserva intacta la "huella dactilar" estadística del idioma original (por ejemplo, la alta frecuencia de la letra 'E' en inglés). Si el texto cifrado es lo suficientemente extenso, herramientas de criptoanálisis pueden mapear estos patrones estadísticos y descifrar el mensaje en milisegundos. Además, este reto sirvió para reforzar la atención a los formatos de entrega atípicos en competiciones CTF (banderas crudas).

## REFERENCIAS

- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Cifrado de Sustitución Monoalfabética, Criptoanálisis Estadístico, Análisis de Frecuencias, Banderas en Crudo (Raw Flags).