
## DESCRIPCION
- A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again. Download the message [here](https://challenge-files.cylabacademy.net/library/ceba1af4dd4ee542c226922acd536495ebe14c328fb6766ae3244de7d7deaa2e/message.txt).

## SOLUCION
```

- Se analizó la consigna del reto, la cual describe una variante del desafío anterior pero sin incluir la clave explícita de correspondencia al inicio del archivo.
    
- Se descargó el archivo adjunto `message.txt` mediante el enlace provisto.
    
- Se inspeccionó el contenido en la terminal con los comandos `head` y `tail`:
    
    - Se confirmó que el texto completo correspondía a un cifrado clásico de sustitución monoalfabética.
        
    - El encabezado iniciaba con la frase cifrada: `NDQy (yzkjd qkj nbwdaje dze qsbc) bje b dfwe kq nklwadej...`.
        
    - La línea final contenía el formato de entrega de la bandera cifrado: `... dze qsbc my: bnbvelf{QJ3GA3INF_4774NU5_4J3_N001_26B742EO}`.
        
- **Criptoanálisis (Known-Plaintext Attack y Análisis de Frecuencias):**
    
    - Se reconoció el texto plano subyacente a partir del patrón gramatical estándar:`NDQy (yzkjd qkj nbwdaje dze qsbc)` $\rightarrow$ `CTFs (short for capture the flag)`.
        
    - Asimismo, el prefijo de la bandera identificó directamente la correspondencia de las letras del término base:`bnbvelf` $\rightarrow$ `academy`.
        
    - Con estas deducciones se construyó la tabla de correspondencia directa entre caracteres cifrados y texto claro:
        
        - `b` $\rightarrow$ `a`, `n` $\rightarrow$ `c`, `d` $\rightarrow$ `t`, `z` $\rightarrow$ `h`, `e` $\rightarrow$ `e`, `q` $\rightarrow$ `f`, `s` $\rightarrow$ `l`, `c` $\rightarrow$ `g`
            
        - `Q` $\rightarrow$ `F`, `J` $\rightarrow$ `R`, `G` $\rightarrow$ `Q`, `A` $\rightarrow$ `U`, `I` $\rightarrow$ `N`, `N` $\rightarrow$ `C`, `F` $\rightarrow$ `Y`
            
        - `U` $\rightarrow$ `K`, `O` $\rightarrow$ `B`
            
    - Se aplicó el mapeo a la cadena de la bandera cifrada respetando los dígitos en _leetspeak_ y caracteres no alfabéticos:
        
        - `QJ3GA3INF` $\rightarrow$ `FR3QU3NCY`
            
        - `4774NU5` $\rightarrow$ `4774CK5`
            
        - `4J3` $\rightarrow$ `4R3`
            
        - `N001` $\rightarrow$ `C00L`
            
        - `26B742EO` $\rightarrow$ `26A742EB`
            
- Se implementó un script en Python para aplicar la tabla de sustitución sobre el texto completo y reconstruir el archivo original:
    
    Python
    
    ```
    cipher_flag = "bnbvelf{QJ3GA3INF_4774NU5_4J3_N001_26B742EO}"
    
    # Diccionario derivado del texto plano conocido
    mapping = {
        "b": "a",
        "n": "c",
        "v": "d",
        "e": "e",
        "l": "m",
        "f": "y",
        "Q": "F",
        "J": "R",
        "G": "Q",
        "A": "U",
        "I": "N",
        "N": "C",
        "F": "Y",
        "U": "K",
        "O": "B",
        "B": "A",
    }
    
    plain_flag = "".join(mapping.get(c, c) for c in cipher_flag)
    print(f"[+] Bandera descifrada: {plain_flag}")
    ```
```

## NOTAS ADICIONALES
Ataques de Texto Plano Conocido (*Known-Plaintext Attack*) en Cifrados Monoalfabéticos: 1. **Preservación de Frecuencias y Patrones:** A diferencia de los cifrados polialfabéticos (como Vigenère) o los algoritmos modernos por bloques (AES), una sustitución simple mantiene constante la relación uno a uno entre caracteres. Esto permite romper la clave sin necesidad de fuerza bruta, deduciendo las letras mediante trigramas/palabras comunes (`the`, `that`, `for`) o la estructura conocida de los formatos de bandera (`picoCTF{...}` o `academy{...}`). 2. **Uso de Herramientas Automatizadas:** Para textos más extensos o sin formato predecible, herramientas basadas en estadísticas de n-gramas del idioma inglés (como `quipqiup`) o algoritmos de escalada de colinas (*hill-climbing algorithm*) logran converger hacia la clave correcta de forma casi instantánea.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium). - Autor: Will Hong. - Conceptos aplicados: Cifrado de Sustitución Monoalfabética, Ataque de Texto Plano Conocido (Known-Plaintext), Análisis de Frecuencias en Criptografía Clásica.