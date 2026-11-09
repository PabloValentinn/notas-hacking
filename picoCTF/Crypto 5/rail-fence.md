
## DESCRIPCION
- A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it? Download the message [here](https://challenge-files.cylabacademy.net/library/d6cea3d41550d2d3e365dd3a7ea99fe9b44fe5fa437d1c921b5134a2070894a5/message.txt).

The decoded message names a phrase. Put that phrase, and nothing else, in the academy flag format: `academy{phrase}`.

## SOLUCION
```

- Se analizó el desafío basado en el cifrado clásico por transposición **Rail Fence Cipher** (cifrado en zigzag), donde la descripción especificó explícitamente el uso de una clave de 4 rieles (_rails = 4_).
    
- Se descargó el archivo `message.txt` provisto mediante el enlace del reto.
    
- **Criptoanálisis y Descifrado:**
    
    - El cifrado Rail Fence no sustituye caracteres, sino que altera su orden escribiendo el mensaje diagonalmente en zigzag a lo largo de un número fijo de filas y leyendo luego horizontalmente cada fila.
        
    - Para invertir el proceso, se modeló una matriz de dimensiones $4 \times L$ (siendo $L$ la longitud total del texto cifrado) para reconstruir el patrón de rebote (_zigzag_).
        
    - Se implementó un script en Python para colocar marcadores en las coordenadas del patrón, rellenar secuencialmente las posiciones marcadas con los caracteres del texto cifrado fila por fila y, finalmente, reconstruir el texto plano leyendo a lo largo del recorrido en zigzag:
        
        Python
        
        ```
        with open("message.txt") as f:
            cipher = f.read().strip()
        
        rails = 4
        n = len(cipher)
        
        # Marcar el patrón geométrico en zigzag
        pattern = [[None] * n for _ in range(rails)]
        row, step = 0, 1
        for col in range(n):
            pattern[row][col] = "*"
            if row == 0:
                step = 1
            elif row == rails - 1:
                step = -1
            row += step
        
        # Asignar los caracteres cifrados fila por fila
        idx = 0
        for r in range(rails):
            for c in range(n):
                if pattern[r][c] == "*" and idx < n:
                    pattern[r][c] = cipher[idx]
                    idx += 1
        
        # Leer el mensaje en zigzag para obtener el texto plano
        plain = []
        row, step = 0, 1
        for col in range(n):
            plain.append(pattern[row][col])
            if row == 0:
                step = 1
            elif row == rails - 1:
                step = -1
            row += step
        
        print("".join(plain))
        ```
        

```
- La ejecución del algoritmo reveló la frase en texto plano: `WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_43BBCEC4`.
- Siguiendo las directrices del reto, se encapsuló la frase resultante dentro del formato de bandera requerido: `academy{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_43BBCEC4}`.
``


## NOTAS ADICIONALES
- Cifrados Clásicos por Transposición: A diferencia de los cifrados por sustitución (como César, ROT13 o Atbash), los algoritmos de transposición conservan la distribución de frecuencia original de las letras pero destruyen su orden secuencial (n-gramas). En el cifrado Rail Fence, la secuencia periódica completa de un ciclo tiene una longitud de $2 \times (\text{rails} - 1)$ pasos. Al ser el espacio de claves extremadamente reducido cuando el número de rieles es pequeño, es un sistema vulnerable a fuerza bruta o reconstrucción matricial directa.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium). 
- Conceptos aplicados: Cifrado por Transposición, Rail Fence Cipher, Algoritmos Matriciales en Python, Reconstrucción de Texto en Zigzag.