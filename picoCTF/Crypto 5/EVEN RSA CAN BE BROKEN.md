
## DESCRIPCION
- This service provides you an encrypted flag. Can you decrypt it with just N & e?

## SOLUCION
```

- Se analizó la consigna del reto y el servicio interactivo desplegado a través de Netcat en el puerto 28330.
    
- El servidor entrega los parámetros públicos de RSA ($N$ y $e$), junto con el texto cifrado $c$ que contiene la bandera oculta.
    
- **Criptoanálisis del ataque (Chosen-Ciphertext Attack / Homomorfismo Multiplicativo de RSA):**
    
    - Al no poder factorizar $N$ directamente por la magnitud de sus números primos, se aprovecha la propiedad homomórfica multiplicativa inherente a RSA sin esquema de relleno (_unpadded/textbook RSA_):
        
        $$E(m_1) \cdot E(m_2) \equiv (m_1)^e \cdot (m_2)^e \equiv (m_1 \cdot m_2)^e \equiv E(m_1 \cdot m_2) \pmod N$$
        
    - Si el servicio interactivo actúa como un oráculo de descifrado que rechaza procesar el texto cifrado exacto de la bandera ($c$), es posible realizar un ataque de texto cifrado escogido (_Chosen-Ciphertext Attack - CCA_) mediante la técnica de cegado (_RSA Blinding_):
        
        1. Se elige un factor entero arbitrario pequeño (por ejemplo, $k = 2$).
            
        2. Se calcula un texto cifrado alternativo $c'$ multiplicando $c$ por $k^e \pmod N$:
            
            $$c' \equiv c \cdot (k^e) \pmod N$$
            
        3. Como $c' \neq c$, el oráculo del servidor acepta procesar $c'$ y devuelve el valor descifrado intermedio $m'$:
            
            $$m' \equiv (c')^d \equiv (c \cdot k^e)^d \equiv (m^e \cdot k^e)^d \equiv m \cdot k \pmod N$$
            
        4. Con el resultado $m'$ devuelto por el servicio, se elimina el factor multiplicativo calculando:
            
            $$m \equiv m' \cdot k^{-1} \pmod N \quad \text{o simplemente} \quad m = \frac{m'}{2}$$
            
- Se implementó la automatización de la interacción con el servicio remoto mediante un script en Python (utilizando `pwntools` o `socket`):
    
    Python
    
    ```
    from pwn import *
    
    # Conexión al servicio remoto
    io = remote("xebec.cylabacademy.net", 28330)
    
    # Lectura de parámetros provistos por el servicio
    io.recvuntil(b"N: ")
    N = int(io.recvline().strip())
    io.recvuntil(b"e: ")
    e = int(io.recvline().strip())
    io.recvuntil(b"c: ")
    c = int(io.recvline().strip())
    
    # Cálculo del texto cifrado cegado (Blinded Ciphertext) con k = 2
    k = 2
    c_blind = (c * pow(k, e, N)) % N
    
    # Envío del texto cifrado modificado al oráculo
    io.sendlineafter(b": ", str(c_blind).encode())
    io.recvuntil(b": ")
    m_prime = int(io.recvline().strip())
    
    # Recuperación del mensaje original
    m = (m_prime * pow(k, -1, N)) % N
    flag = m.to_bytes((m.bit_length() + 7) // 8, byteorder="big").decode("utf-8")
    print(f"[+] Bandera: {flag}")
    ```
```
## NOTAS ADICIONALES
- Vulnerabilidad a Texto Cifrado Escogido (CCA) y Maleabilidad en RSA: 1. **Maleabilidad Criptográfica:** El cifrado RSA elemental es maleable: transformar el texto cifrado genera una transformación predecible en el texto plano resultante sin necesidad de conocer la clave privada $d$. 2. **Mitigación Estándar:** Para evitar ataques de oráculo o cegado homomórfico en sistemas de producción, es obligatorio utilizar esquemas de relleno probabilístico óptimo como **RSA-OAEP** (*Optimal Asymmetric Encryption Padding*), el cual rompe la estructura algebraica multiplicativa impidiendo manipular el texto cifrado sin invalidar la verificación del bloque de datos.

## REFERENCIAS
- Reto original: picoCTF 2025 - Categoría: Cryptography (Easy)[cite: 10]. - Conceptos aplicados: Ataque de Texto Cifrado Escogido (CCA), Maleabilidad Homomórfica de RSA, Cegado Criptográfico (RSA Blinding), Interacción con Servicios en Red (`pwntools`)[cite: 10].
