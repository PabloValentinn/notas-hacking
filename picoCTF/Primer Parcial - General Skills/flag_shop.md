
## DESCRIPCION
- There's a flag shop selling stuff, can you buy a flag? [Source](https://challenge-files.cylabacademy.net/library/a9edd9c3aadfadd003393ce86e6129100aa0d80aa289547175d0609a2c3744a1/store.c). Connect with `nc chatelaine.cylabacademy.net 26727`.
## SOLUCION
```

- Se estableció conexión con el servidor de la tienda mediante la herramienta Netcat (`nc chatelaine.cylabacademy.net 26727`).
    
- Al revisar el menú interactivo, se observó que la bandera verdadera ("1337 Flag") tenía un costo de 100,000 dólares, mientras que el saldo inicial de la cuenta era de solo 1,100 dólares.
    
- Se analizó la lógica de la tienda y se identificó una potencial vulnerabilidad de Desbordamiento de Enteros (Integer Overflow) en la opción de compra de las banderas falsas ("Defintely not the flag Flag"), las cuales costaban 900 dólares cada una.
    
- Se seleccionó la opción de comprar banderas falsas y se solicitó una cantidad exageradamente alta (en este caso, decenas de millones).
    
- Al multiplicar esta cantidad gigante por el costo individual (900), el resultado superó el límite de almacenamiento de un número entero de 32 bits con signo (aprox. 2.14 mil millones). Esto provocó que el valor "diera la vuelta" y se registrara como un costo total negativo.
    
- El programa restó este costo negativo del saldo inicial (ej. `Saldo - (-Costo)`), lo que matemáticamente resultó en una suma, otorgando un saldo de cientos de millones de dólares a la cuenta.
    
- Con los nuevos fondos ilimitados, se regresó al menú principal, se seleccionó la opción para comprar la "1337 Flag", y el sistema entregó exitosamente la bandera.
```

## NOTAS ADICIONALES
- - **Desbordamiento de Enteros (Integer Overflow):** Es una vulnerabilidad crítica que ocurre cuando una operación aritmética genera un valor que excede el espacio de memoria asignado para almacenarlo. En lenguajes como C, si las variables no se validan correctamente, exceder el límite positivo máximo de un entero con signo (signed integer) causa que el bit más significativo cambie, transformando el número en negativo.
    
- **Impacto Crítico:** Aunque este es un reto de CTF, este exacto mismo error de validación (ausencia de _boundary checks_) ha sido responsable de pérdidas millonarias en el mundo real, afectando sistemas bancarios, economías de videojuegos multijugador y, muy recientemente, robos masivos en contratos inteligentes (Smart Contracts) de criptomonedas.

## REFERENCIAS
- - Reto original: **picoCTF 2019** - Categoría: _General Skills_ (flag_shop).
    
- Base de datos de vulnerabilidades: **CWE-190** (Integer Overflow or Wraparound).