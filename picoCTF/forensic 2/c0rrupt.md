
## DESCRIPCION

- We found this [file](https://challenge-files.cylabacademy.net/library/8388ecc430588d15064755583476bec46e23d42a6d8de6e8995c19e40f2e4c58/c0rrupt-mystery). Recover the flag.
## SOLUCION

```

- Se descargó el archivo y, al no ser reconocido por el sistema operativo, se abrió con un editor hexadecimal (`hexedit`).
    
- **Reparación del Magic Number:** Se detectó que la firma principal del archivo estaba destruida. Se sobrescribieron los primeros 8 bytes por la firma estándar de un archivo PNG: `89 50 4E 47 0D 0A 1A 0A`.
    
- Se utilizó la herramienta `pngcheck -v` para ir descubriendo los errores en cascada dentro de los bloques (chunks) de la imagen.
    
- **Reparación del IHDR:** El primer error indicó un nombre de chunk inválido `C"DR` (`43 22 44 52`). Se editó para restaurar el nombre correcto de la cabecera: `IHDR` (`49 48 44 52`).
    
- **Reparación del pHYs:** El programa arrojó un error de CRC (discrepancia matemática) en el bloque físico. Se buscó el bloque `pHYs` en el editor hexadecimal y se cambió el byte de la coordenada que estaba corrupto como `AA` por el valor correcto `00`.
    
- **Reparación del IDAT:** El diagnóstico mostró un error por longitud de bloque demasiado grande y un error de descompresión (zlib buffering error). Se ubicó el inicio del bloque de datos de la imagen y se aplicaron dos correcciones simultáneas:
    
    - Se ajustó el tamaño corrupto de `AA AA FF A5` a su tamaño real de `00 00 FF A5`.
        
    - Se reparó el nombre del bloque que estaba alterado, cambiándolo a `IDAT` (`49 44 41 54`).
        
- Tras estas correcciones, `pngcheck` arrojó el mensaje "No errors detected". Se abrió el archivo de imagen reparado con un visor gráfico, obteniendo la flag escrita sobre la imagen: `picoCTF{c0rrupt10n_1847995}`.
```

## NOTAS ADICIONALES
 - - **Herramientas utilizadas:** `hexedit` (para la manipulación de bytes en crudo) y `pngcheck` (como validador y diagnosticador de la integridad estructural del archivo PNG).
    
- **Estructura PNG:** Este reto es un excelente ejercicio para comprender que los archivos PNG funcionan mediante bloques ("chunks"). Cada bloque contiene 4 partes: Longitud (4 bytes), Nombre del bloque (4 bytes en ASCII), Datos (tamaño variable) y un CRC o código de redundancia cíclica (4 bytes).
    
- **Errores zlib:** Al intentar colocar un tamaño de bloque incorrecto en el `IDAT`, aprendimos que el descompresor "zlib" falla (error -5) porque intenta leer los bytes del siguiente bloque como si fueran colores de la imagen.

## REFERENCIAS
- - Reto original: **picoCTF 2019** - Categoría: _Forensics_ (c0rrupt).
    
- Manual de la herramienta `pngcheck` ([http://www.libpng.org/pub/png/apps/pngcheck.html](http://www.libpng.org/pub/png/apps/pngcheck.html)).
    
- Documentación oficial y estructura de datos del formato Portable Network Graphics (PNG) Specification (W3C).
