

## DESCRIPCION
 - Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure—an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.cylabacademy.net/library/b32f1f1945481591df61d328d02995fe3521d16b70928fbe44e3bd90c4ccb113/confidential.pdf) and uncover the flag within the metadata.

## SOLUCION
```

- Se descargó el archivo PDF provisto (`confidential.pdf`).
    
- **Inspección de Metadatos:**
    
    - Se utilizaron herramientas de análisis forense como `pdfinfo` y `exiftool` para examinar las propiedades internas del documento.
        
    - Se encontró una cadena sospechosa codificada en Base64 en el campo del autor (`Author`): `YWNhZGVteXtwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV85ZDNjYzY2OX0=`.
        
- **Decodificación:**
    
    - Se decodificó la cadena utilizando Base64 para revelar el texto plano:
        
        Bash
        
        ```
        echo "YWNhZGVteXtwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV85ZDNjYzY2OX0=" | base64 -d
        ```
        
- **Bandera:** `academy{puzzl3d_m3tadata_f0und!_9d3cc669}`.
```

## NOTAS ADICIONALES
- **Análisis de Metadatos en Documentos:** Los campos estándar de metadatos en documentos PDF (como Autor, Título, Productor o Asunto) son frecuentemente utilizados en retos forenses de CTF para ocultar información sensible, credenciales o banderas codificadas en esquemas comunes como Base64 o Hex.
## REFERENCIAS
- Reto original: picoMini by CMU-Africa - Categoría: Forensics (Easy).
    
- Autor: Prince Niyonshuti N..