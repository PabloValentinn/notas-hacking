
## DESCRIPCION
- This file doesn't look like much... just a bunch of 1s and 0s. But maybe it's not just random noise. Can you recover anything meaningful from this? Download the file [here](https://challenge-files.cylabacademy.net/library/4f119c7324ffc27875b984a1d0db0591c4214fa81bd566946f1d08ed29f35135/digits.bin).

## SOLUCION
```

- Se descargó el archivo del reto (`digits.bin`).
    
- **Análisis de la Secuencia Binaria:**
    
    - Se examinaron los primeros caracteres y la longitud total del archivo (`71312` caracteres compuestos exclusivamente por `0` y `1`).
        
    - Al agrupar los primeros bits en bloques de 8 (1 byte):
        
        - `11111111` $\rightarrow$ `0xFF`
            
        - `11011000` $\rightarrow$ `0xD8`
            
        - `11111111` $\rightarrow$ `0xFF`
            
        - `11100000` $\rightarrow$ `0xE0`
            
        - `01001010 01000110 01001001 01000110` $\rightarrow$ `JFIF`
            
    - La secuencia coincide con la cabecera (_magic bytes_) estándar de una imagen JPEG/JFIF (`FF D8 FF E0 ... JFIF`).
        
- **Reconstrucción del Archivo Binario:**
    
    - Se convirtió la cadena continua de bits a bytes reales y se exportó como imagen utilizando Python:
        
        Bash
        
        ```
        python3 -c "
        with open('digits.bin', 'r') as f:
            bits = ''.join(f.read().split())
        data = bytes(int(bits[i:i+8], 2) for i in range(0, len(bits), 8))
        with open('flag.jpg', 'wb') as out:
            out.write(data)
        print('[+] Archivo reconstruido exitosamente como flag.jpg')
        "
        ```
        
- **Extracción de la Bandera:**
    
    - Al abrir y visualizar el archivo reconstruido `flag.jpg` (o buscar cadenas de texto dentro de él), se recupera la bandera del reto.
```

## NOTAS ADICIONALES
- **Representación Binaria en ASCII:** En ocasiones los retos forenses almacenan archivos ejecutables o imágenes como representaciones de texto plano de bits (`1` y `0`). Reconocer patrones iniciales como `1111111111011000` (`FF D8` para JPEG) o `1000100101010000` (`89 50` para PNG) permite identificar el tipo de archivo subyacente y reconstruir el archivo binario agrupando cada 8 bits en un byte.

## REFERENCIAS
- Reto original: picoCTF 2026 - Categoría: Forensics (Easy).
    
- Autor: Yahaya Meddy.