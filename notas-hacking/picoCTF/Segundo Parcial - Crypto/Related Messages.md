

## DESCRIPCIÓN
- Oops! I have a typo in my first message so i sent it again! I used RSA twice so this is secure right? [chall.py](https://challenge-files.cylabacademy.net/library/d33371f1a01fd9671ac08d9ce0a486325fd0e8ed66ce83fc97ee9a5a07a64cb9/chall.py) [output.txt](https://challenge-files.cylabacademy.net/library/d33371f1a01fd9671ac08d9ce0a486325fd0e8ed66ce83fc97ee9a5a07a64cb9/output.txt)
## SOLUCION
```

- Se descargaron los artefactos `chall.py` y `output.txt`. Los datos revelan dos criptogramas ($c_1, c_2$), el módulo $N$, un exponente pequeño $e=17$ y la diferencia numérica exacta entre los mensajes planos: $m_1 - m_2 = -3$, lo que establece la relación $m_2 = m_1 + 3$.
    
- **Criptoanálisis (Ataque de Franklin-Reiter):**
    
    - Cifrar dos mensajes relacionados algebraicamente bajo el mismo módulo $N$ permite extraer el mensaje original calculando el Máximo Común Divisor (MCD) de dos polinomios en $\mathbb{Z}_N$:
        
        $$f_1(x) = x^{17} - c_1 \pmod N$$
        
        $$f_2(x) = (x + 3)^{17} - c_2 \pmod N$$
        
    - La raíz común de ambos polinomios es el mensaje $m_1$, por lo que su MCD resulta en el polinomio lineal $x - m_1$.
        
- **Corrección del Error Tipográfico:**
    
    - El MCD recuperó el primer mensaje $m_1$: `academy{m3ssage_w1th_typ0z`.
        
    - Como indica la descripción, el primer mensaje contenía un error. El mensaje corregido $m_2$ equivale a $m_1 + 3$. Al sumar 3 al valor ASCII del último carácter `z` (122), se obtiene 125, correspondiente al carácter `}`.
        
- **Bandera:** `academy{m3ssage_w1th_typ0}`.
```

## NOTAS ADICIONALES
- **Vulnerabilidad de Mensajes Relacionados:** El ataque de Franklin-Reiter demuestra que RSA puro (Textbook RSA) es inseguro. Reenviar un mensaje tras corregir un simple error tipográfico compromete el criptosistema y permite la recuperación del texto claro en tiempo polinomial.

## REFERENCIAS
- Reto: picoCTF 2026 - Cryptography (Medium).
    
- Autor: Philip Thayer.