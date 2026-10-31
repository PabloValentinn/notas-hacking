

## DESCRIPCION

- Can you decrypt this message? Decrypt this [message](https://challenge-files.cylabacademy.net/library/1415ede8e9f58b36fddf7b520d73c151a53ac100c476ca97c7a19f9b901100d3/cipher.txt) using this key "CYLAB".

## SOLUCION
```

- Se analizó la consigna del reto, correspondiente al cifrado polialfabético clásico de Vigenère, el cual especifica de forma explícita la clave de descifrado: `"CYLAB"`.
    
- Se descargó el archivo con el texto cifrado provisto a través del hipervínculo del reto.
    
- **Criptoanálisis y Descifrado:**
    
    - El cifrado de Vigenère aplica múltiples rotaciones tipo César de forma cíclica según los valores alfabéticos de la clave.
        
    - Para cada carácter alfabético en la posición $i$ del texto cifrado, la operación de descifrado modular consiste en:
        
        $$P_i = (C_i - K_i) \pmod{26}$$
        
        donde $C_i$ es el índice del carácter cifrado ($A=0, \dots, Z=25$) y $K_i$ es el índice del carácter correspondiente de la clave repetida `"CYLAB"`. Los caracteres no alfabéticos (números, guiones bajos y llaves) no sufren alteración ni consumen el índice de la clave.
        
    - Se implementó un script en Python para procesar el archivo y aplicar la transformación modular respetando mayúsculas y minúsculas:
        
        Python
        
        ```
        key = "CYLAB"
        with open("cipher.txt", "r") as f:
            ciphertext = f.read()
        
        plaintext = []
        k_idx = 0
        for char in ciphertext:
            if char.isupper():
                shift = ord(key[k_idx % len(key)].upper()) - ord("A")
                plaintext.append(chr((ord(char) - ord("A") - shift) % 26 + ord("A")))
                k_idx += 1
            elif char.islower():
                shift = ord(key[k_idx % len(key)].upper()) - ord("A")
                plaintext.append(chr((ord(char) - ord("a") - shift) % 26 + ord("a")))
                k_idx += 1
            else:
                plaintext.append(char)
        
        flag = "".join(plaintext).strip()
        print(f"[+] Bandera descifrada: {flag}")

```



## NOTAS ADICIONALES

Cifrado Polialfabético de Vigenère: 1. **Ruptura de la Frecuencia Monoalfabética:** A diferencia de los cifrados por sustitución simple, Vigenère utiliza varios alfabetos desplazados, logrando aplanar la distribución de frecuencia de una sola letra (un mismo carácter en texto plano puede cifrarse con distintas letras según su posición respecto a la clave). 2. **Vulnerabilidades y Criptoanálisis:** Aunque durante siglos se le conoció como *le chiffre indéchiffrable*, el cifrado es vulnerable si no se conoce la clave mediante el examen de Kasiski o el cálculo del Índice de Coincidencia (IC) de William F. Friedman, los cuales permiten deducir la longitud de la clave $L$ y descomponer el criptograma en $L$ cifrados César independientes. Al proporcionarse la clave directamente en este desafío[cite: 8], la solución se reduce a una traslación modular inversa directa.
## REFERENCIAS

- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium)[cite: 8]. 
- Autor: Mubarak Mikail[cite: 8]. 
- Conceptos aplicados: Cifrado Polialfabético de Vigenère, Aritmética Modular, Scripts de Decodificación en Python[cite: 8].