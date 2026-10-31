
## DESCRIPCION
- In RSA d is a lot bigger than e, why don't we use d to encrypt instead of e?

## SOLUCION
```

- Se analizó el planteamiento del reto, el cual sugiere de forma ingenua intercambiar los roles de los exponentes de RSA: utilizar la clave privada $d$ (un número grande) para cifrar en lugar del exponente público estándar $e$.
    
- **Análisis matemático:**
    
    En el criptosistema RSA, los exponentes son inversos multiplicativos simétricos módulo $\phi(N)$:
    
    $$e \cdot d \equiv 1 \pmod{\phi(N)}$$
    
    Si el sistema cifra un mensaje $M$ usando la clave privada $d$ para generar el texto cifrado ($C \equiv M^d \pmod N$), la operación que revierte el proceso y recupera el texto plano es elevar al exponente $e$:
    
    $$M \equiv C^e \pmod N$$
    
- Al publicar el valor de $d$ (etiquetado en el servidor como $e$) para que cualquiera pueda verificar o procesar el mensaje, el exponente necesario para descifrar pasa a ser el $e$ original del sistema.
    
- En la inmensa mayoría de las implementaciones criptográficas y librerías estándar (como OpenSSL o PyCryptodome), el exponente público por defecto es el número primo de Fermat **$e = 65537$** ($0x10001$).
    
- Además, al ser $65537$ un valor sumamente pequeño comparado con el módulo $N$ ($d_{descifrado} < \frac{1}{3} N^{1/4}$), la clave de descifrado es completamente vulnerable tanto a una prueba directa con valores estándar como al ataque de fracciones continuas de **Wiener** (Wiener's Attack).
    
- Se estableció la conexión remota con el servicio interactivo mediante Netcat:
    
    Bash
    
    ```
    nc xebec.cylabacademy.net 48335
    ```
    
- El servicio devolvió los valores de $c$, $n$ y el exponente extendido proporcionado.
    
- Se implementó un script en Python (`solve_bootleg.py`) para calcular la exponenciación modular rápida probando el exponente estándar $65537$:
    
    Python
    
    ```
    c = ...  # ciphertext entregado por el servidor
    n = ...  # módulo n entregado por el servidor
    
    # Desencriptación directa usando el exponente estándar original
    m = pow(c, 65537, n)
    
    # Conversión de entero a texto plano
    flag = m.to_bytes((m.bit_length() + 7) // 8, byteorder="big").decode(
        "utf-8", errors="ignore"
    )
    print(flag.strip())
    ```
```

## NOTAS ADICIONALES
- Exponente Privado Débil y Ataque de Wiener: La aparente complejidad de RSA a menudo confunde a quienes asumen que números más grandes siempre significan mayor seguridad. En este reto, invertir las llaves destruye el criptosistema por dos razones: 1. **Clave predecible:** El exponente $65537$ se elige universalmente por razones de rendimiento computacional (solo contiene dos bits en 1: $2^{16} + 1$). Si se convierte en la clave secreta de descifrado, un atacante solo tiene que probar este valor estándar sin necesidad de realizar ningún cálculo avanzado. 2. **Ataque de Wiener:** Si el creador hubiese elegido un exponente secreto pequeño arbitrario en lugar de $65537$, el teorema de Michael J. Wiener (1990) demuestra que cuando $d < \frac{1}{3}N^{1/4}$, la fracción $\frac{e}{N}$ aproxima a $\frac{k}{d}$, permitiendo recuperar la clave privada en tiempo polinomial mediante el desarrollo en fracciones continuas.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Hard)[cite: 10]. - Conceptos aplicados: Simetría de Exponentes RSA, Clave Privada Corta (Small Private Exponent), Ataque de Wiener, Exponente de Fermat $F_4$ ($65537$).
