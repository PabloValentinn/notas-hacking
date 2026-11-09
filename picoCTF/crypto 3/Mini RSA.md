

## DESCRIPCION
- What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M∗∗e)(M∗∗e) is just barely larger than NN. Let's decrypt this: [values](https://challenge-files.cylabacademy.net/library/28a2479cff9eab20837067152fcead0a079e378b38249280192aef28a975269a/values)

## SOLUCION
```
# Función nativa para convertir números a texto (sin importar librerías externas)
def long_to_bytes(n):
    return n.to_bytes((n.bit_length() + 7) // 8, byteorder='big')

# 1. PEGA TUS NÚMEROS AQUÍ
N = # PEGA TU NÚMERO N GIGANTE AQUÍ
e = 3
C = # PEGA TU NÚMERO c GIGANTE AQUÍ

# 2. Función matemática para sacar raíces gigantes sin perder precisión
def integer_nth_root(x, n):
    high = 1
    while high ** n < x:
        high *= 2
    low = high // 2
    while low < high:
        mid = (low + high) // 2
        if low < mid and mid**n < x:
            low = mid
        elif high > mid and mid**n > x:
            high = mid
        else:
            return mid
    return mid + 1

print("Iniciando ataque de raíz cúbica...")

# 3. Probamos iteraciones (vueltas del reloj modular)
for k in range(10):
    # Calculamos el objetivo: Cifrado + (vueltas * Modulo)
    target = C + (k * N)
    
    # Le sacamos la raíz cúbica
    root = integer_nth_root(target, e)
    
    # Si la raíz al cubo es exactamente igual a nuestro objetivo, hackeado.
    if root ** e == target:
        print(f"\n[+] ¡Éxito! Mensaje encontrado en la iteración k={k}")
        
        # Convertimos el número resultante a texto y limpiamos espacios en blanco
        flag = long_to_bytes(root)
        print("[+] Bandera:", flag.decode('utf-8', errors='ignore').strip())
        break

- Se analizó la descripción del reto, que referenciaba una debilidad clásica en la implementación de RSA: el uso de un exponente público muy pequeño (en este caso $e=3$) combinado con un relleno (padding) insuficiente.
    
- Matemáticamente, la encriptación RSA se define como $C \equiv M^e \pmod N$. Si el mensaje $M$ es pequeño y no está correctamente rellenado, $M^3$ será menor que $N$, por lo que el módulo no tiene efecto de envoltura y el mensaje se recupera sacando una raíz cúbica simple.
    
- La pista indicaba que la operación resultó "apenas más grande que $N$", lo que significa que el reloj de la operación modular dio muy pocas vueltas. La fórmula para revertirlo es $M^3 = C + (k \cdot N)$, donde $k$ es un número pequeño de iteraciones.
    
- Se desarrolló un script en Python (`rsahak.py`) diseñado para iterar sobre distintos valores de $k$ y aplicar un algoritmo nativo de búsqueda binaria (`integer_nth_root`) capaz de extraer raíces cúbicas exactas de números gigantes sin perder precisión por coma flotante.
    
- Ante la ausencia de la librería externa `pycryptodome` en el entorno, se implementó una función nativa `long_to_bytes` utilizando métodos de bits estándar de Python (`n.to_bytes`).
    
- Al ejecutar el script, el algoritmo identificó la raíz exacta en la iteración $k=0$ (lo que demostró que el ciphertext original $C$ proporcionado era literalmente $M^3$ en crudo sin haber dado ni una sola vuelta al módulo $N$).
    
- La conversión del entero resultante a texto plano reveló exitosamente la bandera: `academy{e_sh0u1d_b3_lArg3r_35f26e1a}`.
  
  
```

## NOTAS ADICIONALES
- El Ataque del Exponente Pequeño (Small Exponent Attack): Este vector de ataque demuestra por qué es crítico implementar esquemas de relleno seguros, como OAEP (Optimal Asymmetric Encryption Padding), en criptografía de clave pública. Si un sistema utiliza $e=3$ por cuestiones de velocidad de procesamiento, un atacante no necesita intentar factorizar $N$ (un proceso matemáticamente inviable). Simplemente puede tratar la encriptación como un problema de álgebra básica, iterar sobre el módulo unas cuantas veces y destruir la confidencialidad extrayendo la raíz.
## REFERENCIAS

- Reto original: picoCTF 2021 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Criptografía RSA, Small Exponent Attack, Operaciones Modulares, Búsqueda Binaria de Raíces, Python Scripting.