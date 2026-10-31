

## DESCRIPCION
- Can you get sense of this code file and write the function that will decode the given encrypted file content.

Find the encrypted file here [flag_info](https://challenge-files.cylabacademy.net/library/98cdf4861b6c249cc4b06324768d9fbe57cc1cd8512fce4d03595601f380fc0f/enc_flag) and [code file](https://challenge-files.cylabacademy.net/library/98cdf4861b6c249cc4b06324768d9fbe57cc1cd8512fce4d03595601f380fc0f/custom_encryption.py) might be good to analyze and get the flag.

## SOLUCION
```


- Se descargaron e inspeccionaron el script `custom_encryption.py` y el archivo con los datos cifrados `enc_flag` con parámetros $a = 94$, $b = 22$ y la lista `cipher`.
    
- **Análisis de las capas de cifrado:**
    
    1. _Intercambio Diffie-Hellman reducido:_ Utiliza los parámetros globales fijos $p = 97$ y $g = 31$. La clave compartida se deriva calculando $shared\_key = g^{a \cdot b} \pmod p = 31^{94 \cdot 22} \pmod{97} = 81$.
        
    2. _Multiplicación escalar:_ Cada elemento $c_i$ de `cipher` se generó mediante $c_i = \text{ord}(s_i) \times shared\_key \times 311$. La operación inversa es $\text{ord}(s_i) = c_i / (81 \times 311)$.
        
    3. _XOR Dinámico e Inversión:_ El texto plano original se invirtió antes de aplicarle una operación XOR carácter a carácter contra la clave periódica `"trudeau"`.
        
- **Script de descifrado:**
    
    Python
    
    ```
    p, g = 97, 31
    a, b = 94, 22
    text_key = "trudeau"
    cipher = [
        226719,
        1687797,
        1637415,
        50382,
        25191,
        100764,
        1763370,
        1712988,
        1612224,
        1058022,
        0,
        2090853,
        529011,
        125955,
        1712988,
        0,
        554202,
        2166426,
        25191,
        1561842,
        604584,
        680157,
        151146,
        151146,
        428247,
        151146,
        654966,
        302292,
        629775,
        579393,
        428247,
        125955,
        151146,
        0,
    ]
    
    shared_key = pow(g, a * b, p)
    semi_cipher = [chr(c // (shared_key * 311)) for c in cipher]
    rev_plain = [
        chr(ord(c) ^ ord(text_key[i % len(text_key)]))
        for i, c in enumerate(semi_cipher)
    ]
    flag = "".join(rev_plain)[::-1]
    print(flag)
    ```
    

```
- **Bandera:** `academy{custom_d2cr0pt6d_203edf41}` (o `picoCTF{custom_d2cr0pt6d_203edf41}`).
```
```

## NOTAS ADICIONALES
- **Inseguridad por reducción de parámetros:** La implementación de Diffie-Hellman sobre un módulo primo diminuto ($p = 97$) carece de seguridad criptográfica; el espacio es tan pequeño que cualquier atacante puede resolver el secreto por fuerza bruta en milisegundos, incluso si los exponentes $a$ y $b$ no fuesen revelados explícitamente en el archivo de salida. - **Reversibilidad determinista:** Al no existir operaciones unidireccionales con pérdida de información (como funciones de dispersión criptográfica o truncamientos modulares con ambigüedad), toda la cadena de transformaciones es invertible paso a paso.

## REFERENCIAS
- Reto original: picoCTF 2024 - Categoría: Cryptography (Medium). 
- Autor: NGIRIMANA Schadrack
- Conceptos aplicados: Intercambio de Claves Diffie-Hellman, Aritmética Modular, Cifrado XOR Dinámico, Inversión de Cadenas.