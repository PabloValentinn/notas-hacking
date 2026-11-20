
## DESCRIPCION
- Can you get the flag? Download this [binary](https://challenge-files.cylabacademy.net/library/4923664c378efee1cf819f12d90c49c484d3749bfebe4e0c13976ca588154f37/gdbme).

Here's the test drive instructions:

- `$ chmod +x gdbme`
- `$ gdb gdbme`
- `(gdb) layout asm`
- `(gdb) break *(main+99)`
- `(gdb) run`
- `(gdb) jump *(main+104)`

## SOLUCION
```

- Se descargó el archivo binario `gdbme` y se le asignaron permisos de ejecución mediante `chmod +x gdbme`.
    
- **Análisis y Manipulación Dinámica con GDB:**
    
    - Se cargó el ejecutable en el depurador mediante `gdb gdbme` y se activó la vista de instrucciones en ensamblador con `layout asm`.
        
    - Se inspeccionó el flujo de la función `main`, identificando una llamada bloqueante a la función `sleep` (`<sleep@plt>`) antes de la rutina de descifrado (`rotate_encrypt`).
        
    - Se estableció un punto de interrupción justo antes de dicha instrucción utilizando `break *(main+99)` y se inició la ejecución con `run`.
        
    - Una vez detenido el flujo en el _breakpoint_, se forzó el salto del puntero de instrucción (_RIP_) hacia la dirección posterior a la llamada bloqueante mediante `jump *(main+104)`.
        
    - El programa reanudó su ejecución normal, descifró la cadena en memoria e imprimió la bandera en consola.
        
- **Bandera:** `academy{d3bugg3r_dr1v3_4cc75120}`
```

## NOTAS ADICIONALES
- **Depuración Dinámica y Alteración del Flujo:** Herramientas como **GDB** (_GNU Debugger_) permiten inspeccionar el estado de los registros y la memoria en tiempo real. El uso de _breakpoints_ combinados con la instrucción `jump` demuestra cómo es posible evadir mecanismos de retardo, validaciones o trampas _anti-debugging_ modificando directamente el flujo de ejecución del procesador sin necesidad de parchar el archivo binario en disco.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Reverse Engineering (Medium).
    
- Autor: LT 'syreal' Jones
