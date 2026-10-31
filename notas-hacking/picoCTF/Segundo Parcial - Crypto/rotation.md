
## DESCRIPCION
- You will find the flag after decrypting this file Download the encrypted flag [here](https://challenge-files.cylabacademy.net/library/7b27068b4f8daca5e159c2ee99494b77c9f8418a8576d6a0cabc7947d41577aa/encrypted.txt).

## SOLUCION
```

- Se analizó la consigna del reto correspondiente a criptografía clásica basada en rotación de caracteres alfabéticos (Cifrado César / ROT-N).
    
- Se descargó el archivo `encrypted.txt` provisto mediante el hipervínculo del reto.
    
- Se examinó el archivo cifrado en la terminal:
    
    Bash
    
    ```
    cat encrypted.txt
    ```
    
    Se observó una cadena cifrada que mantenía intactos los delimitadores (`{}`), números y guiones bajos (`_`), cuyo prefijo alfabético correspondía a una traslación directa del formato estándar de bandera (`xqkwKBN{...}` o similar).
    
- **Criptoanálisis y Descifrado:**
    
    - El cifrado César opera desplazando cada letra del abecedario un número entero fijo $k$ de posiciones módulo 26:
        
        $$C_i = (P_i + k) \pmod{26}$$
        
    - Al comparar las letras del prefijo cifrado con el prefijo esperado (`picoCTF` o `academy`), se identificó una diferencia de desplazamiento constante de 8 posiciones ($k = 8$).
        
    - Para invertir el cifrado y recuperar el texto original, se aplicó la traslación inversa:
        
        $$P_i = (C_i - 8) \pmod{26} \equiv (C_i + 18) \pmod{26}$$
        
    - Se implementó un script en Python para aplicar la rotación sobre los 26 desplazamientos posibles o revertir directamente la rotación de 8 posiciones:
        
        Python
        
        ```
        with open("encrypted.txt", "r") as f:
          ciphertext = f.read().strip()
        
        shift = 8
        plaintext = []
        for c in ciphertext:
          if c.isupper():
            plaintext.append(chr((ord(c) - ord("A") - shift) % 26 + ord("A")))
          elif c.islower():
            plaintext.append(chr((ord(c) - ord("a") - shift) % 26 + ord("a")))
          else:
            plaintext.append(c)
        
        flag = "".join(plaintext)
        print(f"[+] Bandera descifrada: {flag}")
        ```
        

```
  - La reversión alfabética expuso el texto plano del mensaje: `picoCTF{r0tat1on_d3crypt3d_7952

academy{r0tat1on_d3crypt3d_42440c4b}


## NOTAS ADICIONALES
Cifrado por Desplazamiento (César / ROT-N):
1. **Espacio de Claves Reducido:** A diferencia de los cifrados monoalfabéticos generales que cuentan con $26! \approx 4 \times 10^{26}$ claves posibles, el cifrado César limita el espacio de búsqueda a únicamente 25 desplazamientos no triviales ($k \in [1, 25]$). Esto convierte a cualquier variante de rotación en un esquema completamente vulnerable a ataques exhaustivos de fuerza bruta en milisegundos. 
2. **Preservación de Entropía Estructural:** La rotación alfabética pura no altera caracteres no alfabéticos (como dígitos o símbolos de puntuación) ni modifica la longitud de las palabras. Esta característica facilita la identificación inmediata de patrones de texto plano conocido (*known-plaintext*) al inspeccionar la estructura exterior de formatos de banderas o sintaxis léxica.

## REFERENCIAS

- Reto original: picoCTF 2023 - Categoría: Cryptography (Medium)[cite: 12]. 
- Autor: Loic Shema[cite: 12].
- Conceptos aplicados: Cifrado César, Rotación Alfabética Modular (ROT-N), Fuerza Bruta sobre Espacios de Claves Finos, Criptoanálisis Clásico[cite: 12].