
## DESCRIPCION
- You will find the flag after analysing this apk Download [here](https://challenge-files.cylabacademy.net/library/b31248aec6287cbe220d0dbfa55e216b87e6175b3561d441062bfdd018f3cacc/timer.apk).

## SOLUCION
```

- Se descargó el archivo ejecutable de Android provisto (`timer.apk`).
    
- **Extracción del APK:**
    
    - Sabiendo que un archivo APK funciona como un archivo comprimido estándar, se extrajo su contenido directamente utilizando:
        
        Bash
        
        ```
        unzip -q timer.apk -d extracted/
        ```
        
- **Análisis Estático y Búsqueda:**
    
    - Se realizó una búsqueda recursiva del formato de la bandera utilizando `grep`. El sistema indicó una coincidencia dentro del archivo binario `classes3.dex` (`grep: extracted/classes3.dex: binary file matches`).
        
- **Extracción de la Bandera:**
    
    - Se leyeron las cadenas de texto plano (_strings_) directamente desde el archivo `.dex` (Dalvik Executable) compilado, filtrando el prefijo de la bandera para obtener la solución exacta:
        
        Bash
        
        ```
        strings extracted/classes3.dex | grep -E "(picoCTF|academy)\{"
        ```
```

## NOTAS ADICIONALES
- **Análisis Rápido de APKs:** En retos de ingeniería inversa en Android, si la bandera u otros secretos están integrados directamente en el código (_hardcoded_) sin ofuscación o cifrado, no siempre es necesario utilizar descompiladores complejos como `jadx`. El uso de utilidades nativas de Linux como `unzip` y `strings` sobre los archivos `.dex` permite una recuperación ágil y directa.

## REFERENCIAS
- Reto original: picoCTF 2023 - Categoría: Reverse Engineering (Medium).
    
- Autor: Loic Shema.
