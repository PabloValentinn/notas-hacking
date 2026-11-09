
## DESCRIPCION
- What does asm3(0xba75113d,0xdc9e1676,0xe2b51af6) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format. [Source](https://challenge-files.cylabacademy.net/library/ee7fbe47c75c8fb71e77f6d84d1a85101db3f80d5ddb63bac143bc2c0ac45977/test.S)

## SOLUCION
```

- Se examinó estáticamente el código fuente en ensamblador x86 (`test.S`).
    
- **Análisis de Manipulación de Registros y Endianness:**
    
    - Se mapearon en memoria los tres argumentos de 32 bits considerando la arquitectura _Little-Endian_.
        
    - El algoritmo inicializa el acumulador general `eax` en cero mediante un XOR consigo mismo.
        
    - El programa realiza operaciones aritméticas y de bits extrayendo fragmentos muy específicos de la memoria mediante el uso de apuntadores a bytes (`BYTE PTR`) y palabras (`WORD PTR`).
        
    - Se simuló el estado de los sub-registros de 8 y 16 bits (`al`, `ah`, `ax`) instrucción por instrucción:
        
        1. Se cargó `0x75` en `ah`.
            
        2. Se desplazó (Shift Left) `ax` por `0x10` posiciones, lo que efectivamente vació el registro `ax` a `0x0000`.
            
        3. Se restó `0x76` a `al`, provocando un desbordamiento que dejó el sub-registro en `0x8a`.
            
        4. Se sumó `0x16` a `ah`, dejando la porción de 16 bits (`ax`) con el valor `0x168a`.
            
        5. Se aplicó la operación de disyunción exclusiva (XOR) entre `ax` y los primeros dos bytes del tercer parámetro (`0x1af6`).
            
    - El cálculo final de la operación `0x168a ^ 0x1af6` determinó que el valor remanente en `eax` al llegar al `ret` es `0x0c7c` (o simplemente `0xc7c`).
        
- **Bandera:** `0xc7c`.
```
## NOTAS ADICIONALES
- **Complejidad Arquitectónica en x86:** Este nivel requiere comprender profundamente cómo un registro de 32 bits (`eax`) se subdivide en componentes más pequeños (`ax`, `ah`, `al`) y cómo las operaciones sobre una subsección afectan el valor global. Adicionalmente, resalta la importancia de recordar cómo se distribuyen los bytes en memoria, ya que `WORD PTR` invierte el orden lógico debido a la convención _Little-Endian_.

## REFERENCIAS

- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Hard).
    
- Autor: Sanjay C...