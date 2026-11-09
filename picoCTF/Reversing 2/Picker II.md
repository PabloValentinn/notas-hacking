

## DESCRIPCION
- Can you figure out how this program works to get the flag?

## SOLUCION
```
- Se estableció conexión con el servicio mediante el comando `nc xebec.cylabacademy.net 40121`.
    
- **Análisis de Restricciones:** A diferencia del primer reto, esta versión implementaba un filtro basado en listas negras (_blacklist_) que bloqueaba explícitamente el uso de la palabra `win`, impidiendo invocar la función de forma directa.
    
- **Inyección de Código Python:** Dado que el programa seguía procesando y ejecutando la entrada del usuario como instrucciones dinámicas de Python, se explotó la vulnerabilidad utilizando funciones integradas del lenguaje (_built-ins_) para leer el sistema de archivos del servidor de manera arbitraria.
    
    - Se introdujo el siguiente comando para leer e imprimir el contenido del archivo de la bandera:
        
        Python
        
        ```
        print(open('flag.txt').read())
        ```
        
- **Bandera:** `academy{f1l73r5_f41l_c0d3_r3f4c70r_m1gh7_5ucc33d_bd7d479d}`.

```

## NOTAS ADICIONALES
-  **Ineficacia de Listas Negras:** Filtrar cadenas de texto específicas (como bloquear nombres de funciones) es una contramedida débil cuando se utilizan mecanismos de evaluación dinámica de código como `eval()` o `exec()`. Los atacantes siempre pueden evadir el filtro utilizando llamadas a nivel del sistema operativo, manipulación de módulos (como `os` o `sys`) o funciones nativas de manipulación de archivos (`open()`, `read()`).


## REFERENCIAS
- Reto original: picoCTF - Categoría: Reverse Engineering (Easy).
    
- Autor: LT 'syreal' Jones.