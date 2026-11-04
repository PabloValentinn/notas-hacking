

## DESCRIPCION
- This service can provide you with a random number, but can it do anything else?

## SOLUCION
```

- Se estableció conexión con el servidor mediante el comando `nc chatelaine.cylabacademy.net 33652`.
    
- **Explotación Dinámica:** Se determinó que el programa invoca funciones de Python dinámicamente basándose en la entrada del usuario. Se introdujo el comando `win` para forzar la ejecución de la función oculta en lugar de las opciones regulares.
    
- **Decodificación de la Bandera:** La función `win` retornó la solución codificada en una secuencia hexadecimal separada por espacios (`0x61 0x63 0x61...`). Se convirtieron los valores hexadecimales a caracteres ASCII utilizando un decodificador.
    
- **Bandera:** `academy{4_d14m0nd_1n_7h3_r0ugh_193d362d}`.
```

## NOTAS ADICIONALES
- **Vulnerabilidad de Invocación (Python):** Utilizar la entrada directa del usuario para resolver y llamar funciones dentro del entorno (por ejemplo, a través de `eval()`, `exec()` o manipulación de atributos) permite a los atacantes acceder a funciones críticas, no documentadas o de depuración.

## REFERENCIAS
- Reto original: picoCTF - Categoría: Reverse Engineering (Easy).
    
- Autor: LT 'syreal' Jones.
