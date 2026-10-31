
## DESCRIPCION
- Why use p and q when I can use more? Connect with `nc xebec.cylabacademy.net 18662`.

## SOLUCION
```
- Se analizó el planteamiento del reto, donde el creador alteró el algoritmo tradicional de generación de llaves RSA. En lugar de utilizar dos números primos gigantescos ($p$ y $q$) para calcular el módulo $N$, decidió utilizar múltiples números primos mucho más pequeños ($N = p_1 \cdot p_2 \cdot p_3 \dots p_k$).
    
- Se estableció conexión con el servidor a través de Netcat (`nc xebec.cylabacademy.net 18662`), obteniendo el texto cifrado ($c$), el módulo ($n$) y el exponente público estándar ($e = 65537$).
    
- **Análisis de vulnerabilidad:** La seguridad del algoritmo RSA recae en que el tamaño de sus factores primos sea lo suficientemente grande para resistir ataques de factorización. Al dividir la misma longitud de bits del módulo $N$ entre muchos factores, el tamaño individual de cada número primo se reduce drásticamente, volviéndolos vulnerables a algoritmos de criba cuadrática o búsqueda en bases de datos.
    
- Se extrajo el valor de $n$ y se ingresó en la base de datos de números primos **FactorDB**, logrando factorizar el módulo gigante casi instantáneamente en una lista extensa de números primos pequeños.
    
- Con todos los factores $p_i$ expuestos, se calculó la función fi de Euler ($\phi$) utilizando su forma generalizada para múltiples primos:
    
    $$\phi(N) = (p_1 - 1) \cdot (p_2 - 1) \cdot (p_3 - 1) \dots (p_k - 1)$$
    
- Una vez obtenido el valor de $\phi(N)$, se procedió a calcular la llave privada $d$ mediante el inverso multiplicativo modular del exponente público: $d \equiv e^{-1} \pmod{\phi(N)}$.
    
- Se aplicó la operación de descifrado estándar $M \equiv c^d \pmod N$ y se convirtió el entero resultante a texto legible (ASCII/UTF-8).
    
- La decodificación exitosa reveló el mensaje oculto, entregando la bandera del desafío: `academy{too_many_fact0rs_0164780}`.



academy{too_many_fact0rs_0164780}
```

## NOTAS ADICIONALES
- Multi-Prime RSA: Aunque la variante de RSA con múltiples primos existe en la criptografía real (descrita en estándares como PKCS#1 v2.1) y se usa para acelerar el proceso de descifrado utilizando el Teorema Chino del Resto (CRT), requiere que se utilicen normalmente solo 3 o 4 primos, y que cada uno de ellos siga siendo criptográficamente masivo. Si se abusa de este concepto (como en este reto) reduciendo el tamaño de los primos para poder agregar "más cantidad", el tiempo necesario para romper el módulo $N$ cae en picada, ya que el esfuerzo de factorización depende del factor primo más pequeño, no de la cantidad de factores.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Hard).
    
- Conceptos aplicados: Multi-prime RSA, Factorización de Módulo, FactorDB, Función Totiente de Euler Generalizada, Inverso Multiplicativo Modular.