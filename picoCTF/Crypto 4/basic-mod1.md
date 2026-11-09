
## DESCRIPCION
- We found this weird message being passed around on the servers, we think we have a working decryption scheme. Download the message [here](https://challenge-files.cylabacademy.net/library/153c6663b971f4d124ad181fdbf1c21ad47dc241b7a578ab47253d6461f2f145/message.txt).

Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.

Wrap your decrypted message in the academy flag format (i.e. `academy{decrypted_message}`)

## SOLUCION
- Se analizó la descripción del desafío, la cual detallaba el esquema exacto de descifrado basado en aritmética modular y mapeo de caracteres:
    
    - Cada número entero contenido en el archivo descargable debe reducirse mediante la operación residuo módulo 37 ($n \pmod{37}$).
        
    - El resultado numérico (en el rango de 0 a 36) se mapea a un conjunto finito de 37 símbolos:
        
        - `0` – `25`: Letras del abecedario en mayúsculas (`A`–`Z`).
            
        - `26` – `35`: Dígitos decimales (`0`–`9`).
            
        - `36`: Carácter guion bajo (`_`).
            
- Se descargó el archivo `message.txt`, el cual contenía una secuencia de números enteros separados por espacios.
    
- Se desarrolló un script en Python (`solve_mod1.py`) para automatizar la lectura de los datos, la reducción modular y la concatenación del texto resultante:
    
    Python
    
    ```
    import string
    
    # Definición del conjunto de 37 caracteres indexados del 0 al 36
    charset = string.ascii_uppercase + string.digits + "_"
    
    # Lectura y conversión de los enteros del archivo
    with open("message.txt", "r") as f:
        numbers = [int(x) for x in f.read().split()]
    
    # Reducción modular y reconstrucción del texto plano
    decrypted = "".join(charset[n % 37] for n in numbers)
    
    # Formateo de la bandera requerida por la plataforma
    flag = f"academy{{{decrypted}}}"
    print(f"[+] Bandera: {flag}")
    ```

## NOTAS ADICIONALES
- Aritmética Modular y Cifrados de Sustitución: La reducción módulo $m$ comprime un espacio numérico infinito a un conjunto finito $\{0, 1, \dots, m-1\}$, principio fundamental en algoritmos criptográficos (como RSA, Diffie-Hellman y curvas elípticas). En este reto se implementa una versión digital de un cifrado de sustitución polialfabético o monoalfabético mapeado, donde el espacio modular 37 acomoda exactamente el alfabeto en inglés (26), los dígitos decimales (10) y un separador de palabras (1).

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium)[cite: 10]. 
- Conceptos aplicados: Aritmética Modular ($n \pmod{37}$), Mapeo de Caracteres Alfanuméricos, Automatización con Scripts en Python[cite: 10].