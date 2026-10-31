
## DESCRIPCION
- Someone encrypted a message using AES in ECB mode but they weren’t very careful with their key. Turns out it’s derived from something as simple as the current time! Can you uncover the key and decrypt the flag? Download the encrypted message: [message](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/message.txt)  
You may also find the encryption script helpful: [code](https://challenge-files.cylabacademy.net/library/838909e4e064bca5edc41edd46ebb4f8350eb82f2aea2540ea564e491c6d437e/encryption.py)

## SOLUCION
```

- Se descargaron e inspeccionaron el script `encryption.py` y el archivo `message.txt`.
    
- **Análisis de la Derivación de Clave:**
    
    - El algoritmo cifra el mensaje en modo **AES-128-ECB** aplicando relleno PKCS#7.
        
    - La clave de 16 bytes se deriva tomando el hash SHA-256 de una marca de tiempo UNIX en formato entero (`int(time.time())`):
        
        $$\text{key} = \text{SHA256}(\text{str}(timestamp))[:16]$$
        
    - El archivo `message.txt` proporciona una pista con la marca de tiempo aproximada: `1790147519` UTC, junto con el criptograma en hexadecimal `44e98ac8b821d1b561b49f38c114c89405c1895b1f9425b6adc8e0911b68731a`.
        
- **Descifrado:**
    
    - El cifrado se realizó exactamente en el segundo indicado en la pista ($\text{offset} = 0$).
        
    - Se derivó la clave de 128 bits calculando el SHA-256 de `"1790147519"` y se descifró el texto con OpenSSL:
        
        Bash
        
        ```
        python3 -c '
        from hashlib import sha256
        import subprocess
        
        ts = 1790147519
        ct_hex = "44e98ac8b821d1b561b49f38c114c89405c1895b1f9425b6adc8e0911b68731a"
        key_hex = sha256(str(ts).encode()).hexdigest()[:32]
        
        cmd = ["openssl", "enc", "-d", "-aes-128-ecb", "-K", key_hex, "-nopad"]
        p = subprocess.Popen(cmd, stdin=subprocess.PIPE, stdout=subprocess.PIPE)
        out, _ = p.communicate(bytes.fromhex(ct_hex))
        
        pad_len = out[-1]
        flag = out[:-pad_len].decode()
        print(flag)
        '
        ```
        
- **Bandera:** `academy{sa3S_sEc9t_3b464909}`.
```

## NOTAS ADICIONALES
- **Baja entropía en generación de claves (CWE-330 / CWE-337):** Utilizar marcas de tiempo como semilla o fuente directa para material criptográfico elimina la seguridad del cifrado, ya que reduce el espacio de búsqueda a una pequeña ventana temporal vulnerable a ataques de fuerza bruta en segundos.
    
- **Inseguridad del modo AES-ECB:** El modo Electronic Codebook (ECB) no utiliza vector de inicialización (IV) y cifra bloques idénticos en salidas idénticas, exponiendo patrones del texto claro.

## REFERENCIAS
- Reto original: picoCTF 2026 - Categoría: Cryptography (Medium).
    
- Autor: Yahaya Meddy.
    
- Conceptos aplicados: Cifrado Simétrico AES-128-ECB, Derivación Débil de Claves con Timestamps, Hashing SHA-256, Padding PKCS#7.