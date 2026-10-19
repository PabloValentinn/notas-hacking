
## DESCRIPCION
- In RSA, a small ee value can be problematic, but what about NN? Can you decrypt this? [values](https://challenge-files.cylabacademy.net/library/c800df9c0f52301295a618b2bff7362cf61388e5a04f135b01c9693fdf7a09e8/values)

## SOLUCION
```
- Se analizó la premisa del reto, la cual planteaba una vulnerabilidad derivada del tamaño insuficiente del módulo $N$.
    
- Se descargó el archivo `values`, extrayendo los componentes de la encriptación: el texto cifrado ($c$), el exponente público ($e$) y el módulo ($N$).
    
- Dado que la seguridad de RSA depende de que factorizar $N$ sea computacionalmente inviable, un valor de $N$ de longitud reducida permite recuperar sus factores primos fundamentales ($p$ y $q$).
    
- Se ingresó el valor de $N$ en la base de datos de números primos **FactorDB**, descomponiéndolo exitosamente en sus factores:
    
    $$N = p \cdot q$$
    
- Con $p$ y $q$ expuestos, se calculó la función fi de Euler ($\phi(N)$):
    
    $$\phi(N) = (p - 1) \cdot (q - 1)$$
    
- Se calculó el exponente privado de descifrado $d$ mediante el inverso modular de $e$ respecto a $\phi(N)$ ($d \equiv e^{-1} \pmod{\phi(N)}$) usando funciones aritméticas nativas (`pow(e, -1, phi)` en Python).
    
- Se ejecutó el descifrado estándar de RSA para obtener el mensaje original en formato numérico:
    
    $$M \equiv c^d \pmod N$$
    
- Finalmente, se convirtió el entero resultante $M$ a formato de texto plano (ASCII/UTF-8), extrayendo la bandera: `academy{sma11_N_n0_g0od_a3ac7152}`.

academy{sma11_N_n0_g0od_a3ac7152}
```

## NOTAS ADICIONALES
- El Problema de Factorización de Enteros: La seguridad asimétrica de RSA se basa en que multiplicar dos primos grandes es instantáneo, pero dividir su producto de vuelta en sus factores originales requiere un tiempo impráctico con claves seguras (de 2048 o 4096 bits). Cuando se emplea un módulo $N$ débil o generado con claves cortas, herramientas de cribado de números (como GNFS o bases de datos como FactorDB) rompen la clave pública en segundos. Al encontrar $p$ y $q$, cualquier receptor no autorizado puede reconstruir la llave privada $d$ y descifrar todo el tráfico interceptado.

## REFERENCIAS

- Reto original: picoCTF 2021 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Criptosistema RSA, Factorización de Módulo $N$, FactorDB, Función Totiente de Euler, Inverso Multiplicativo Modular.