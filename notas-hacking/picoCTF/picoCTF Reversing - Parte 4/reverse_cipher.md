
## DESCRIPCION
- We have recovered a [binary](https://challenge-files.cylabacademy.net/library/39f6c4e22fa904f6aca954775da252beb639f0266a3a8d9107b6f8644cc853f3/rev) and a [text file](https://challenge-files.cylabacademy.net/library/39f6c4e22fa904f6aca954775da252beb639f0266a3a8d9107b6f8644cc853f3/rev_this). Can you reverse the flag.

## SOLUCION
```

- Se inspeccionó el archivo de texto `rev_this`, obteniendo la cadena cifrada de 24 bytes: `academy{w1{1wq8c7_h4846}`.
    
- **Análisis de Ensamblador Estático (`objdump`):**
    
    - Se desensambló la función `main` del ejecutable `rev` mediante `objdump -d -M intel rev`.
        
    - Se identificó que el binario lee `0x18` (24) caracteres y los procesa en tres segmentos:
        
        1. Los primeros 8 caracteres (índices `0` a `7`) se copian intactos al archivo de salida.
            
        2. Del índice `8` al `22` (`0x16`), el algoritmo verifica la paridad del índice mediante una operación `AND` con `0x1`: a los índices pares les suma `0x5` (`add eax, 0x5`) y a los índices impares les resta `0x2` (`sub eax, 0x2`).
            
        3. El carácter final (índice `23`, ubicado en `[rbp-0x39]`) se escribe sin modificaciones.
            
- **Reversión del Cifrado:**
    
    - Se aplicó el algoritmo inverso (restando `5` a las posiciones pares y sumando `2` a las impares entre los índices `8` y `22`) mediante un script en Python:
        
        Python
        
        ```
        cipher = "academy{w1{1wq8c7_h4846}"
        flag = list(cipher)
        for i in range(8, 23):
            flag[i] = chr(ord(cipher[i]) - 5) if i % 2 == 0 else chr(ord(cipher[i]) + 2)
        print("".join(flag))
        ```
        
- **Bandera:** `academy{r3v3rs3e2ac6361}`.
```

## NOTAS ADICIONALES
- **Cifrados Personalizados en Binarios:** En ingeniería inversa, los algoritmos de cifrado simétrico simples basados en desplazamientos ASCII dependen de la posición del byte en memoria. Identificar las instrucciones aritméticas (`add`, `sub`) y las máscaras de bits (`and 0x1` para determinar paridad) permite reconstruir la función inversa exacta.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Hard).
    
- Autor: Danny Tunitis.