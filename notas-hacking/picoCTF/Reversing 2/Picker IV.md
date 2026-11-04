

## DESCRIPCION
- Can you figure out how this program works to get the flag?
## SOLUCION
```
- Se descargó el archivo binario compilado `picker-IV` y su código fuente en C.
    
- **Análisis de Símbolos:** Se utilizó la utilidad `nm` para inspeccionar la tabla de símbolos del binario y localizar la dirección de la función oculta:
    
    Bash
    
    ```
    nm picker-IV | grep win
    ```
    
- Se determinó que la función `win` se encontraba alojada en la dirección de memoria hexadecimal `4012a1`.
    
- **Explotación del Flujo de Control:** Se estableció conexión con el servidor mediante el comando `nc chatelaine.cylabacademy.net 28818`.
    
- Al solicitar un destino, se ingresó el valor `4012a1`, forzando al programa a saltar a dicha dirección y ejecutar la rutina para devolver la bandera.
```

## NOTAS ADICIONALES

- **Salto Arbitrario a Memoria:** A diferencia de las inyecciones dinámicas en Python de los retos anteriores, este escenario demuestra una vulnerabilidad crítica a bajo nivel. El binario vulnerable toma el input del usuario y lo invoca directamente como un puntero a función, permitiendo a un atacante redirigir la ejecución hacia cualquier segmento de memoria existente.
## REFERENCIAS

- Reto original: picoCTF - Categoría: Binary Exploitation (Medium).
    
- Autor: LT 'syreal' Jones.