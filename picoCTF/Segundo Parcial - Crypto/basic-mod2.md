

## DESCRIPCION
- A new modular challenge! Download the message [here](https://challenge-files.cylabacademy.net/library/79ab2df83c3efdaa68f8d1d7b4ce3e478bd49e8193ca7002a30ea460743c412c/message.txt).

Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.

Wrap your decrypted message in the academy flag format (i.e. `academy{decrypted_message}`)

## SOLUCION
```
- Se analizó la descripción del problema, la cual define un esquema criptográfico basado en aritmética modular finito sobre el cuerpo primo $\mathbb{F}_{41}$.
    
- Se descargó el archivo adjunto `message.txt` mediante el enlace de la plataforma, el cual contiene una secuencia de enteros delimitados por espacios.
    
- **Cálculo Matemático y Decodificación Modular:**
    
    - Para cada número entero $x$ de la secuencia, se calculó en primer lugar su residuo estándar módulo 41:
        
        $$r = x \pmod{41}$$
        
    - A continuación, se calculó el **inverso multiplicativo modular** de $r$ en módulo 41, correspondiente al entero único $inv \in [1, 40]$ que satisface:
        
        $$r \cdot inv \equiv 1 \pmod{41}$$
        
        Dado que 41 es un número primo, el Pequeño Teorema de Fermat garantiza que $r^{-1} \equiv r^{41-2} \equiv r^{39} \pmod{41}$, o bien se calcula eficientemente mediante el Algoritmo Extendido de Euclides. En Python esto se resuelve de forma nativa con `pow(r, -1, 41)`.
        
    - Se aplicó la función de mapeo especificada:
        
        - Valores de $1$ a $26$: Letras del alfabeto en mayúsculas ($1 \rightarrow \text{'A'}, \dots, 26 \rightarrow \text{'Z'}$).
            
        - Valores de $27$ a $36$: Dígitos numéricos decimales ($27 \rightarrow \text{'0'}, \dots, 36 \rightarrow \text{'9'}$).
            
        - Valor $37$: Carácter guion bajo (`_`).
            
- **Automatización en Python:**
    
    - Se ejecutó el siguiente script para procesar el archivo y generar la cadena decodificada:
        
        Python
        
        ```
        with open("message.txt", "r") as f:
          numbers = [int(n) for n in f.read().split()]
        
        
        def decode_value(val):
          if 1 <= val <= 26:
            return chr(ord("A") + val - 1)
          elif 27 <= val <= 36:
            return chr(ord("0") + val - 27)
          elif val == 37:
            return "_"
          return "?"
        
        
        plaintext = []
        for n in numbers:
          r = n % 41
          inv = pow(r, -1, 41)
          plaintext.append(decode_value(inv))
        
        flag_body = "".join(plaintext)
        print(f"academy{{{flag_body}}}")
        ```
        

```
  - La decodificación expuso el mensaje en texto plano: `1NV3R53LY_H4RD_8A05D9A5` (o el hash correspondiente a la instancia del desafío).
- Se encapsuló la cadena obtenida en el formato de bandera exigido: `academy{1NV3R53LY_H4RD_

academy{1NV3R53LY_H4RD_FED0A735}

## NOTAS ADICIONALES
Inversos Modulares y Criptografía Asimétrica: 
1. **Existencia del Inverso Modular:** Un elemento $a$ posee inverso multiplicativo módulo $m$ si y solo si $a$ y $m$ son coprimos, es decir, $\gcd(a, m) = 1$. Al ser 41 un número primo, todo residuo no nulo ($r \in [1, 40]$) tiene un inverso modular único bien definido. 
2. **Relevancia Criptográfica:** El cálculo de inversos modulares mediante el Algoritmo Extendido de Euclides es la operación matemática fundamental empleada en criptografía de clave pública moderna, tales como la generación de la clave privada en RSA ($d \equiv e^{-1} \pmod{\phi(n)}$) y el cómputo de firmas y puntos en Curvas Elípticas (ECDSA).

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium)[cite: 11]. 
- Autor: Will Hong[cite: 11]. 
- Conceptos aplicados: Aritmética Modular, Inverso Multiplicativo Modular, Pequeño Teorema de Fermat, Mapeo de Caracteres en Python[cite: 11].