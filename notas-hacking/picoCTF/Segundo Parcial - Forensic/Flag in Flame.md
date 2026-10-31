
## DESCRIPCION
- The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Could there be something hidden within? Your mission is to inspect the resulting file and reveal the real purpose of it. The team is relying on your skills to uncover any concealed information within this unusual log. Download the encoded data here: [Logs Data](https://challenge-files.cylabacademy.net/library/e6fc51b98dd61381c5cd54dc836c8344fb475f17728f2095969e3a0f401ea195/logs.txt). Be prepared—the file is large, and examining it thoroughly is crucial .

## SOLUCION
```
- Se analizó el archivo `logs.txt`, identificando que contenía una imagen PNG codificada en Base64 (`iVBORw0KGgo...`).
    
- **Decodificación Base64:**
    
    - Se reconstruyó el archivo de imagen mediante el comando:
        
        Bash
        
        ```
        base64 -d logs.txt > flag.png
        ```
        
- **Decodificación Hexadecimal:**
    
    - Se extrajo la cadena hexadecimal visible dentro de la imagen (`61636164656D797B666F72656E736963735F616E616C797369735F69735F616D617A696E675F32303433646264317D`) y se convirtió a texto ASCII:
        
        Bash
        
        ```
        echo "61636164656D797B666F72656E736963735F616E616C797369735F69735F616D617A696E675F32303433646264317D" | xxd -r -p
        ```
        
- **Bandera:** `academy{forensics_analysis_is_amazing_2043dbd1}`.
```

## NOTAS ADICIONALES
- **Codificación Múltiple (Multi-layer Encoding):** Es habitual en retos forenses combinar esquemas de representación (como Base64 para transportar binarios en texto plano y Hexadecimal dentro de recursos gráficos) para dificultar la detección mediante búsquedas simples con `grep`.
## REFERENCIAS
- Reto original: picoMini by CMU-Africa - Categoría: Forensics (Easy).
    
    image_5482fa.png
    
- Autor: Prince Niyonshuti N..
    
    image_5482fa.png