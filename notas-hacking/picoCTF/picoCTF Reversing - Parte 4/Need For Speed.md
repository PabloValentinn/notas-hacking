

## DESCRIPCION
- The name of the game is [speed](https://www.youtube.com/watch?v=8piqd2BWeGI). Are you quick enough to solve this problem and keep it above 50 mph? [need-for-speed](https://challenge-files.cylabacademy.net/library/fdeee821b25644eec47b7364634c63fec68ebd782883df49c4089d9d2b92303d/need-for-speed)

## SOLUCION
```

- Se descargó el archivo ejecutable `need-for-speed` y se verificó su arquitectura mediante `file`, confirmando que se trataba de un binario ELF de 64 bits dinámicamente enlazado y con su tabla de símbolos intacta (`not stripped`).
    
- **Análisis Estático de Símbolos y Desensamblado:**
    
    - Se inspeccionaron las funciones del programa utilizando `nm need-for-speed | grep " T "`, identificando rutinas clave como `set_timer`, `alarm_handler`, `get_key`, `calculate_key` y `print_flag`.
        
    - Al desensamblar la función `main` con `objdump -d -M intel need-for-speed`, se observó que el flujo principal ejecuta primero `set_timer` (configurando una alarma temporal del sistema) antes de calcular la clave (`get_key`) y mostrar el resultado (`print_flag`), lo que provoca que el proceso aborte por tiempo agotado durante una ejecución normal.
        
- **Manipulación de Señales en Tiempo de Ejecución (GDB):**
    
    - Se asignaron permisos de ejecución al binario con `chmod +x need-for-speed` y se cargó en el depurador mediante `gdb need-for-speed`.
        
    - Dentro de la consola de GDB, se configuró el manejo de señales para evitar que la interrupción del temporizador detuviera el programa:
        
        Fragmento de código
        
        ```
        handle SIGALRM ignore
        ```
        
    - Se inició el proceso con `run`, permitiendo que la función `get_key` completara el cálculo sin ser interrumpida y que `print_flag` imprimiera la bandera en pantalla.
        
- **Bandera:** `academy{Good job keeping bus #31326f14 speeding along!}`.
```

## NOTAS ADICIONALES
- **Manejo de Señales en Sistemas POSIX (`SIGALRM`):** Muchos binarios implementan temporizadores mediante la llamada al sistema `alarm()`, la cual envía una señal `SIGALRM` al proceso tras cumplirse un tiempo límite para finalizar su ejecución. En depuración dinámica con **GDB**, el comando `handle <SEÑAL> ignore` intercepta dicha señal y evita que sea entregada al programa, permitiendo analizar o completar rutinas costosas en tiempo sin necesidad de modificar las instrucciones del ejecutable.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Hard).
    
- Autor: Alexander Bushkin.
