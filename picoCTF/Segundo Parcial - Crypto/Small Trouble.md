


## DESCRIPCION
- Everything seems secure; strong numbers, familiar parameters but something small might ruin it all. Can you recover the message? Download the [message](https://challenge-files.cylabacademy.net/library/3a16f68729491af8a7840a7cc2a1244c8d49b8da749f91330e5cf92516820f1f/message.txt). And source [code](https://challenge-files.cylabacademy.net/library/3a16f68729491af8a7840a7cc2a1244c8d49b8da749f91330e5cf92516820f1f/encryption.py)


## SOLUCION
```

- Se descargaron e inspeccionaron los artefactos `encryption.py` y `message.txt`.
    
- **Criptoanálisis (Ataque de Wiener):**
    
    - El algoritmo genera dos primos de 1048 bits ($n \approx 2096\text{ bits}$), pero genera un exponente privado $d$ de apenas 256 bits (`d = getPrime(256)`).
        
    - Al cumplirse la condición $d < \frac{1}{3} n^{1/4}$ (donde $n^{1/4} \approx 2^{524}$ y $2^{256} \ll \frac{1}{3} 2^{524}$), la fracción $\frac{k}{d}$ aparece entre los convergentes del desarrollo en fracciones continuas de $\frac{e}{n}$.
        
- **Script de descifrado:**
    
    Python
    
    ```
    import math
    
    
    def get_convergents(e, n):
      num1, num2 = 1, 0
      den1, den2 = 0, 1
      x, y = e, n
      while y != 0:
        q = x // y
        x, y = y, x - q * y
        num1, num2 = q * num1 + num2, num1
        den1, den2 = q * den1 + den2, den1
        yield num1, den1
    
    
    for k, d in get_convergents(e, n):
      if k != 0 and (e * d - 1) % k == 0:
        phi = (e * d - 1) // k
        s = n - phi + 1
        disc = s * s - 4 * n
        if disc >= 0:
          root = math.isqrt(disc)
          if root * root == disc and (s + root) % 2 == 0:
            m = pow(c, d, n)
            print(bytes.fromhex(hex(m)[2:]).decode(errors="ignore"))
            break
    ```
    

```
- **Bandera:** `academy{sm4ll_d_073963cb}`.
```
```

## NOTAS ADICIONALES
- **Vulnerabilidad de Exponente Privado Débil:** La optimización de operaciones criptográficas reduciendo el tamaño de $d$ compromete críticamente la seguridad de RSA. La cota teórica de Wiener demuestra que cualquier clave privada con $d < \frac{1}{3} n^{0.25}$ puede reconstruirse en tiempo polinomial.

## REFERENCIAS
- Reto original: picoCTF 2026 
- Categoría: Cryptography (Medium). - Autor: Yahaya Meddy. 
- Conceptos aplicados: Criptoanálisis RSA, Ataque de Wiener, Fracciones Continuas, Teorema de Aproximación de Legendre.