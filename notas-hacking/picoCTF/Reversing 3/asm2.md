
## DESCRIPCION
- What does asm2(0xb,0x1a) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://challenge-files.cylabacademy.net/library/4f21bf6736722e7bba9c981acfe0d42562211fc8b1896f5472ce048faa13a381/test.S)
## SOLUCION
```

- Se analizó estáticamente el código fuente en ensamblador x86 (`test.S`).
    
- **Análisis del Flujo de Ejecución (Dry Run):**
    
    - Se identificó la estructura de un bucle `while` condicionado por una instrucción `jle` (salto si es menor o igual).
        
    - El código inicializa un acumulador (`[ebp-0x4]`) con el valor `0x1a` y un contador límite (`[ebp-0x8]`) con el valor `0xb`.
        
    - El algoritmo instruye sumar `0xe7` iterativamente al contador límite hasta que supere la barrera estática de `0x5ed6`, sumando simultáneamente `0x1` al acumulador en cada ciclo.
        
- **Cálculo del Valor Final:**
    
    - El bucle de suma (`0xb + (iteraciones * 0xe7) <= 0x5ed6`) arrojó un total de 106 ciclos efectivos antes de romper la condición.
        
    - Al sumar estos 106 ciclos al valor base del acumulador (`0x1a` + 106 en base decimal), el registro final almacenado para ser devuelto en `eax` resultó ser `132`, que corresponde a `0x84` en formato hexadecimal.
        
- **Bandera:** `0x84`.
```

## NOTAS ADICIONALES
**Estructuras de Control en Ensamblador:** Este reto evalúa la capacidad de traducir ramificaciones lógicas a nivel máquina en algoritmos de alto nivel. Identificar correctamente las variables locales en la pila, cuál actúa como registro de estado y cuál dicta la condición de ruptura, permite calcular la salida matemáticamente sin necesidad de ensamblar ni ejecutar un binario en vivo.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Hard).
    
- Autor: Sanjay C.