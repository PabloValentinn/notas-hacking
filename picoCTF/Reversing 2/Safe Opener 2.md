

## DESCRIPCION

- What can you do with this file? I forgot the key to my safe but this [file](https://challenge-files.cylabacademy.net/library/867399a60e44754a85257c7eb1afa26731c73afa90daafcd4779710c9fa4a05e/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

## SOLUCION
```

- Se descargó el archivo provisto por el reto (`SafeOpener.class`).
    
- **Identificación del Archivo:**
    
    - Mediante el comando `file SafeOpener.class` se comprobó que correspondía a un binario compilado de Java (_compiled Java class data_).
        
- **Análisis Estático:**
    
    - Al inspeccionar las cadenas legibles dentro del bytecode compilado mediante la herramienta `strings`, se observó que la clave de desbloqueo no estaba ofuscada ni cifrada, encontrándose directamente en texto plano dentro del código:
        
        Bash
        
        ```
        strings SafeOpener.class | grep -E "(picoCTF|academy)\{"
        ```
        
    - De forma alternativa, al descompilar el archivo con `javap -c SafeOpener.class` o descompiladores como CFR/JADX, se confirma la constante hardcodeada en el método de validación.
        
- **Bandera:** `picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_52e008f0}` _(o `academy{SAf3_0p3n3rr_y0u_solv3d_it_52e008f0}` en plataformas con prefijo local)_.
```

## NOTAS ADICIONALES
- **Hardcoded Credentials en Binarios:** A diferencia de la primera versión del reto donde la clave residía codificada en Base64, en ejecutables y clases compiladas es común encontrar secretos y contraseñas expuestos directamente en la tabla de constantes si el desarrollador no implementó protecciones o técnicas de empaquetado/ofuscación. La extracción de cadenas con `strings` suele ser el primer vector de inspección en ingeniería inversa rápida.

## REFERENCIAS

- Reto original: picoCTF 2023 - Categoría: Reverse Engineering (Medium).
    
- Autor: Mubarak Mikail.