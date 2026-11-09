
## DESCRIPCION
- Can you figure out how this program works to get the flag?

## SOLUCION
```
- Se estableció conexión con el servidor mediante el comando `nc chatelaine.cylabacademy.net 39156`.
    
- **Explotación de Sobrescritura de Variables:**
    
    - Mediante el análisis del código fuente y la interacción con la consola, se determinó que la opción `3` del menú principal permitía modificar variables globales o referencias del programa.
        
    - Se utilizó esta vulnerabilidad para sobrescribir la función legítima `getRandomNumber` con el nombre de la función oculta `win`.
        
- **Ejecución y Decodificación:**
    
    - Al invocar la opción `4` (originalmente destinada a generar un número aleatorio), el programa ejecutó la función `win` debido a la sobrescritura de la referencia.
        
    - La función retornó la bandera en formato hexadecimal, la cual fue decodificada a caracteres ASCII.
        
- **Bandera:** `academy{7h15_15_wh47_w3_g37_w17h_u53r5_1n_ch4rg3_948e866e}`.





```

## NOTAS ADICIONALES
- **Secuestro de Flujo de Control en Scripts:** Permitir que los usuarios manipulen los nombres y valores de las variables en un entorno dinámico como Python hace posible redirigir el flujo de control de la aplicación. Este ataque es el equivalente lógico en alto nivel de sobrescribir punteros a funciones (como en un ataque _GOT overwrite_ en C/C++), alterando lo que ejecuta una opción predefinida del menú.
## REFERENCIAS
- Reto original: picoCTF - Categoría: Reverse Engineering (Medium).
    
- Autor: LT 'syreal' Jones.
