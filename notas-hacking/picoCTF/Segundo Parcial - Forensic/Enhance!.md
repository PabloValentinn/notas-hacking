
## DESCRIPCION
- Download this image file and find the flag.

- [Download image file](https://challenge-files.cylabacademy.net/library/e64e2668a8f34ef7ddcbdd713ba52720a8804ff3a0914677983d29a4b48c3e6a/drawing.flag.svg)

## SOLUCION
```

- Se descargó el archivo SVG provisto en el reto (`drawing.flag.svg`).
    
- **Inspección de código fuente:**
    
    - Al tratarse de un archivo vectorial en formato XML, se examinó el código fuente plano del archivo encontrando la sección de texto (`<text>` y `<tspan>`).
        
    - Las letras que componen la bandera se encontraban fragmentadas y separadas por espacios individuales dentro de las etiquetas de texto.
        
    - Al concatenar los caracteres fragmentados (`academy{3 n h 4 n c 3 d _ 9 f 3 1 c 0 4 b}`), se reconstruyó la cadena completa.
        
- **Bandera:** `academy{3nh4nc3d_9f31c04b}`.
```

## NOTAS ADICIONALES
- **Esteganografía en SVG:** Los gráficos vectoriales escalables (SVG) permiten incrustar texto invisible, metadatos o fragmentos de texto con opacidad nula, tamaño diminuto o ocultos tras capas de diseño, siendo una técnica común de ocultamiento en retos de análisis forense digital.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Autor: LT 'syreal' Jones.