

## DESCRIPCION
- A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher? Download the message [here](https://challenge-files.cylabacademy.net/library/0a2e91276318c0f6d400f5096fdaf87fcf57f37ebabf90004552502979a581c8/message.txt).

## SOLUCION
```


- Se analizó la descripción del desafío, la cual plantea un cifrado clásico de sustitución monoalfabética e indica explícitamente que la clave de correspondencia se encuentra ubicada en la primera línea del archivo.
    
- Se descargó el archivo provisto denominado `message.txt` a través del enlace del reto.
    
- Se inspeccionó la estructura del archivo mediante la terminal de comandos:
    
    Bash
    
    ```
    head -n 5 message.txt
    ```
    
    Se verificó que la primera línea correspondía a una permutación de 26 caracteres del alfabeto en mayúsculas (la clave de sustitución), seguida por un texto en inglés cifrado que contiene la bandera estructurada en su párrafo final.
    
- **Criptoanálisis y Descifrado:**
    
    - Al contar con el alfabeto cifrado completo en el encabezado, no fue necesario aplicar técnicas heurísticas de análisis de frecuencia de letras o n-gramas.
        
    - Cada posición $i$ de la cadena clave representa a qué letra del alfabeto inglés estándar (`A-Z`) fue mapeado el texto original.
        
    - Para invertir el proceso, se construyó una tabla de traducción bidireccional (preservando mayúsculas y minúsculas) y se reemplazaron los caracteres del texto cifrado por sus equivalentes del alfabeto estándar:
        
        Python
        
        ```
        import string
        
        with open("message.txt") as f:
            lines = f.read().splitlines()
        
        # La primera línea contiene la clave completa de 26 letras
        key = lines[0].strip()
        ciphertext = "\n".join(lines[1:])
        
        std_upper = string.ascii_uppercase
        std_lower = string.ascii_lowercase
        
        # Mapeo del alfabeto cifrado hacia el alfabeto ordenado convencional
        trans_table = str.maketrans(
            key.upper() + key.lower(), std_upper + std_lower
        )
        plaintext = ciphertext.translate(trans_table)
        
        # Impresión del texto descifrado y extracción de la bandera
        print(plaintext)
        ```
        

```
- La decodificación del bloque final del documento expuso el texto en claro y la bandera del reto: `academy{5UB5717U710N_EV0LU710N_59AEAB80}` (o `picoCTF{5UB5717U710N_EV0LU710N_59AEAB80}`).

## NOTAS ADICIONALES
- Cifrado por Sustitución Monoalfabética: En este esquema criptográfico clásico, cada letra del alfabeto en texto plano se reemplaza por una letra fija de un alfabeto permutado a lo largo de todo el mensaje. Aunque el espacio de claves teóricas es de $26! \approx 4 \times 10^{26}$ (lo que descarta la fuerza bruta pura), el cifrado preserva las propiedades estadísticas y de distribución de frecuencia de los idiomas naturales, haciéndolo vulnerable al análisis de frecuencia si el texto es suficientemente largo. En este reto particular, la exposición de la clave en el propio mensaje (*key disclosure*) eliminó la necesidad de criptoanálisis estadístico, reduciendo la solución a una transcodificación directa de cadenas.
## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium). - Autor: Will Hong. - Conceptos aplicados: Cifrado de Sustitución Monoalfabética, Tablas de Mapeo de Caracteres (`str.maketrans`), Transcodificación de Texto en Python.