
## DESCRIPCION
- It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher? Download the message [here](https://challenge-files.cylabacademy.net/library/696c6874056837b137b48e23a74d72e27d26def4454fdb690063e6baefa68124/message.txt).

## SOLUCION
```
- Se analizó la consigna del reto, correspondiente a la tercera fase de la serie de cifrados por sustitución monoalfabética, caracterizada por la eliminación deliberada de espacios y signos de puntuación tradicionales para dificultar la segmentación léxica.
    
- Se descargó el archivo `message.txt` provisto mediante el hipervínculo de la plataforma.
    
- Se inspeccionó el archivo en la terminal mediante `cat message.txt`, observando una cadena continua de texto en minúsculas que concluía con la estructura formal de la bandera en mayúsculas: `...udmauovwxndwbwiuhq{E6C4H_4E41Q515_15_73I10Z5_9O106F2U}`.
    
- **Criptoanálisis (Análisis de Frecuencias y N-gramas):**
    
    - A pesar de la ausencia de signos de puntuación, el texto preservó íntegramente la frecuencia natural de distribución de letras y la estructura de bigramas/trigramas del idioma inglés.
        
    - La secuencia final permitió identificar el prefijo del formato mediante ataque de texto plano conocido (_Known-Plaintext Attack_):`wbwiuhq{...}` $\rightarrow$ `academy{...}`
        
        - `w` $\rightarrow$ `a`
            
        - `b` $\rightarrow$ `c`
            
        - `i` $\rightarrow$ `d`
            
        - `u` $\rightarrow$ `e`
            
        - `h` $\rightarrow$ `m`
            
        - `q` $\rightarrow$ `y`
            
    - Se identificaron palabras clave recurrentes en el texto continuo sobre competencias de ciberseguridad:
        
        - `mau` $\rightarrow$ `the` ($m \rightarrow t, a \rightarrow h, u \rightarrow e$)
            
        - `ovwx` $\rightarrow$ `flag` ($o \rightarrow f, v \rightarrow l, x \rightarrow g$)
            
        - `nd` $\rightarrow$ `is` ($n \rightarrow i, d \rightarrow s$)
            
        - `bkhgzmucd` $\rightarrow$ `computers` ($k \rightarrow o, g \rightarrow p, z \rightarrow u, c \rightarrow r$)
            
        - `bkhgumnmnked` $\rightarrow$ `competitions` ($e \rightarrow n$)
            
    - Al completar la tabla de sustitución para las letras mayúsculas contenidas en la bandera cifrada:
        
        - `E` $\rightarrow$ `N`
            
        - `C` $\rightarrow$ `R`
            
        - `H` $\rightarrow$ `M`
            
        - `Q` $\rightarrow$ `Y`
            
        - `I` $\rightarrow$ `D`
            
        - `Z` $\rightarrow$ `U`
            
        - `O` $\rightarrow$ `F`
            
        - `F` $\rightarrow$ `B`
            
        - `U` $\rightarrow$ `E`
            
    - Se tradujo la bandera preservando los dígitos en _leetspeak_ y separadores:
        
        - `E6C4H` $\rightarrow$ `N6R4M` (_N-GRAM_)
            
        - `4E41Q515` $\rightarrow$ `4N41Y515` (_ANALYSIS_)
            
        - `15` $\rightarrow$ `15` (_IS_)
            
        - `73I10Z5` $\rightarrow$ `73D10U5` (_TEDIOUS_)
            
        - `9O106F2U` $\rightarrow$ `9F106B2E`
            
- Se implementó un script en Python para aplicar la tabla de sustitución sobre el archivo y verificar el texto completo:
    
    Python
    
    ```
    import string
    
    ciphertext = open("message.txt").read().strip()
    
    # Diccionario derivado del criptoanálisis
    mapping = {
        "m": "t",
        "a": "h",
        "u": "e",
        "c": "r",
        "s": "x",
        "n": "i",
        "d": "s",
        "w": "a",
        "v": "l",
        "k": "o",
        "p": "w",
        "x": "g",
        "b": "c",
        "h": "m",
        "g": "p",
        "z": "u",
        "e": "n",
        "q": "y",
        "f": "b",
        "i": "d",
        "o": "f",
        "l": "k",
        "y": "v",
        "r": "q",
    }
    
    # Expandir el mapeo a mayúsculas
    full_map = {k: v for k, v in mapping.items()}
    full_map.update({k.upper(): v.upper() for k, v in mapping.items()})
    
    plaintext = "".join(full_map.get(char, char) for char in ciphertext)
    print(plaintext[-80:])
    ```
    

```
- La reconstrucción validó la lectura coherente del texto y expuso la bandera final: `academy{N6R4M_4N41Y515_15_73D10U5_9F106B2E}`.



## NOTAS ADICIONALES
- Cifrado Monoalfabético sin Puntuación y Análisis de N-gramas: 1. **Impacto de la Puntuación en el Criptoanálisis:** Suprimir espacios y signos ortográficos evita el reconocimiento directo de longitudes de palabras (aislar artículos o preposiciones cortas como *a*, *an*, *the*, *in*). Sin embargo, no neutraliza la debilidad fundamental de los cifrados monoalfabéticos: las probabilidades condicionales de ocurrencia de pares (bigramas como *TH*, *HE*, *IN*) y secuencias de tres letras (trigramas como *THE*, *AND*, *ING*) se mantienen invariables. 2. **Algoritmos Automatizados (Hill Climbing / Simulated Annealing):** En criptografía clásica, cuando un texto cifrado carece de delimitadores, los motores de resolución automática puntúan posibles claves candidatas comparando la frecuencia de tetragramas del texto descifrado frente a un modelo lingüístico estándar hasta maximizar la verosimilitud estadística del mensaje.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium).
- Autor: Will Hong.
- Conceptos aplicados: Cifrado por Sustitución Monoalfabética, Análisis de N-gramas, Eliminación de Delimitadores de Texto, Mapeo Inverso en Python.