
## DESCRIPCION
- Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message. Download the corrupted message [here](https://challenge-files.cylabacademy.net/library/c432352dd1b936c7ab4ceb162b63dafa1292c57462d832c59614d4db0de130be/message.txt).

## SOLUCION
```

- Se descargó el archivo `message.txt` provisto por el reto.
    
- **Criptoanálisis:** El texto inicia con `heT` , lo que permite inferir que la palabra original de tres letras era `The`. Para invertir la transposición de cada tríada $(c_0, c_1, c_2)$, se reorganiza el bloque en la secuencia `c2 + c0 + c1`.
    
- **Script de descifrado:**
    
    Python
    
    ```
    with open("message.txt") as f:
        data = f.read()
    
    recovered = [
        data[i + 2] + data[i : i + 2] if len(data[i : i + 3]) == 3 else data[i:]
        for i in range(0, len(data), 3)
    ]
    print("".join(recovered))
    ```
    

```
- **Bandera:** `picoCTF{7R4N5P051N6_15_3XP3N51V3_1094142f}` (o `academy{...}` según la plataforma).

academy{7R4N5P051N6_15_3XP3N51V3_5571D3F8}.


## NOTAS ADICIONALES
- **Espacio de estados reducido:** Para bloques de longitud $n=3$ solo existen $3! = 6$ permutaciones posibles, lo que vuelve trivial el ataque mediante texto plano conocido.
## REFERENCIAS

- Reto: picoCTF 2022 - Cryptography (Medium).
- Autor: Will Hong.