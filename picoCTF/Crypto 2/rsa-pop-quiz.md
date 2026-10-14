
## DESCRIPCION

## SOLUCION
```
- Se estableció la conexión inicial al servidor desde la terminal de Kali Linux mediante el comando `nc xebec.cylabacademy.net 47314`, iniciando un cuestionario interactivo sobre los componentes del algoritmo RSA.
    
- **Problema 1 (Calcular módulo $n$):** A partir de los factores primos $p$ y $q$, se calculó el módulo multiplicándolos directamente: $n = p \times q$. (Factible: Sí).
    
- **Problema 2 (Calcular factor $q$):** A partir del módulo $n$ y el factor $p$, se despejó la variable faltante realizando la división exacta: $q = n / p$. (Factible: Sí).
    
- **Problema 3 (Factorizar $n$ en $p$ y $q$):** Se determinó que, dado un exponente público $e$ y un módulo gigante $n$, es criptográficamente inviable encontrar los factores primos originales debido a la complejidad del Problema de Factorización de Enteros. (Factible: No).
    
- **Problema 4 (Calcular función Totient $\phi(n)$):** Teniendo los factores primos $p$ y $q$, se aplicó la fórmula de la indicatriz de Euler: $\phi(n) = (p-1) \times (q-1)$. (Factible: Sí).
    
- **Problema 5 (Cifrar un mensaje $c$):** Teniendo el mensaje en claro $m$, la llave pública $e$ y el módulo $n$, se calculó el criptograma mediante exponenciación modular: $c = m^e \pmod n$. (Factible: Sí).
    
- **Problema 6 (Descifrar solo con $n$):** Se justificó la imposibilidad de recuperar un texto original teniendo como único dato el módulo público $n$, sin texto cifrado ni llaves asociadas. (Factible: No).
    
- **Problema 7 (Calcular llave privada $d$):** Dados $p$, $q$ y $e$, se obtuvo la llave privada calculando el inverso multiplicativo modular del exponente público sobre el valor de la función totient: $d \equiv e^{-1} \pmod{\phi(n)}$. (Factible: Sí).
    
- **Problema 8 (Descifrado final RSA):** El servidor entregó $n, p, e$ y el texto cifrado $c$. Se derivó $q$ por división, se calculó $\phi(n)$ y finalmente la llave privada $d$. Con esto, se descifró el mensaje mediante la fórmula $m = c^d \pmod n$.
    
- El número decimal resultante gigante se convirtió a formato hexadecimal y posteriormente a caracteres de texto (ASCII), revelando la bandera final: `academy{wA8_th4t$_ill3aGal..od365BFb2}`.


academy{wA8_th4t$_ill3aGal..od365BFb2}
```

## NOTAS ADICIONALES
 - Fundamentos y Seguridad de RSA: Este desafío ilustra el funcionamiento interno del criptosistema de clave pública RSA. Demuestra empíricamente que las operaciones de cifrado, descifrado y generación de llaves ("funciones trampa") son extremadamente rápidas (tiempo polinómico) siempre y cuando se conozcan los números primos originales. La seguridad absoluta del algoritmo descansa en el problema ilustrado en la tercera pregunta: si un atacante solo tiene acceso a la llave pública ($n$ y $e$), le resulta computacionalmente imposible factorizar un módulo lo suficientemente grande en un lapso de tiempo útil para extraer la llave privada.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Hard).
    
- Conceptos aplicados: Criptografía Asimétrica, Algoritmo RSA, Aritmética Modular, Problema de Factorización de Enteros, Inverso Multiplicativo Modular.
