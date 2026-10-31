

## DESCRIPCION
- A message was encrypted using a shared secret... but it looks like one side of the exchange leaked something. Can you piece together the secret and get the flag? Download the [message](https://challenge-files.cylabacademy.net/library/70415f267476bdaa5762bdd5dce4d587950c58d1a6105e1244310679bd20de4d/message.txt). And source [code](https://challenge-files.cylabacademy.net/library/70415f267476bdaa5762bdd5dce4d587950c58d1a6105e1244310679bd20de4d/encryption.py)

## SOLUCION
```

- Se descargaron e inspeccionaron los artefactos del reto: el script de generación `encryption.py` y los parámetros resultantes en `message.txt`.
    
- **Análisis Criptográfico:**
    
    - El código implementa un intercambio de claves Diffie-Hellman clásico: el servidor genera una clave privada $a$ y publica $A = g^a \pmod p$, mientras que el cliente genera una clave privada $b$.
        
    - La clave compartida se computa mediante $shared = A^b \pmod p$ y el texto plano se cifra aplicando un XOR byte a byte contra el byte de menor peso de dicha clave ($k = shared \pmod{256}$).
        
    - Se detectó una fuga crítica de parámetros: en lugar de publicar la clave pública del cliente ($B = g^b \pmod p$), el archivo `message.txt` exportó directamente el secreto privado del cliente ($b$).
        
- **Descifrado y Recuperación:**
    
    - Al contar con el módulo primo $p$, la clave pública del servidor $A$ y la clave privada del cliente $b$, se calculó el secreto compartido de forma directa sin requerir resolver el problema del logaritmo discreto:
        
        Bash
        
        ```
        python3 -c '
        with open("message.txt") as f:
            params = dict(line.split(" = ") for line in f.read().strip().split("\n") if " = " in line)
        
        p = int(params["p"])
        A = int(params["A"])
        b = int(params["b"])
        enc = bytes.fromhex(params["enc"])
        
        shared = pow(A, b, p)
        flag = bytes([x ^ (shared % 256) for x in enc]).decode()
        print(flag)
        '
        ```
        
    - La operación XOR inversa reveló la bandera: `academy{dh_s3cr3t_2f0e1b6c}`.
```

## NOTAS ADICIONALES
Seguridad en Intercambio Diffie-Hellman:

1. **Problema del Logaritmo Discreto (DLP):** La solidez del protocolo Diffie-Hellman depende de la impracticabilidad computacional de derivar los exponentes secretos ($a$ o $b$) a partir de los valores públicos intercambiados ($A$ o $B$).
    
2. **Impacto de la Exposición de Secretos:** La filtración involuntaria de una clave privada ($b$) degrada instantáneamente la seguridad del protocolo, permitiendo a cualquier observador pasivo derivar el secreto de sesión compartido ($shared = A^b \pmod p$) mediante una única exponenciación modular.

## REFERENCIAS

- Reto original: picoCTF 2026 - Categoría: Cryptography (Easy).
    
- Autor: Yahaya Meddy.
    
- Conceptos aplicados: Protocolo Diffie-Hellman, Fuga de Claves Privadas, Cifrado por Flujo XOR, Aritmética Modular en Python.