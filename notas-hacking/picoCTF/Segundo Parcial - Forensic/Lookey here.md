

## DESCRIPCION
- Attackers have hidden information in a very large mass of data in the past, maybe they are still doing it. Download the data [here](https://challenge-files.cylabacademy.net/library/1e5b915df467718ade9bc65b9de2094f73159c40c620fbea7bfec17f657252b3/anthem.flag.txt).

## SOLUCION
```

- Se descargó el archivo masivo de texto provisto en el reto.
    
- **Búsqueda forense (`grep`):**
    
    - Utilizando la etiqueta orientativa del reto, se filtró el contenido del archivo mediante una búsqueda por coincidencia de patrones para localizar la estructura de la bandera:
        
        Bash
        
        ```
        grep -r "academy" .
        ```
        
- **Bandera:** `academy{gr3p_15_@w3s0m3_33595e98}`.
```

## NOTAS ADICIONALES
- **Inspección de Archivos Masivos:** El uso de herramientas de línea de comandos como `grep` es fundamental en análisis forense digital y CTFs para filtrar grandes volúmenes de texto (logs, dumps o archivos masivos) y extraer cadenas de texto sensibles o marcadores específicos de manera eficiente.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Autores: LT 'syreal' Jones / Mubarak Mikail.