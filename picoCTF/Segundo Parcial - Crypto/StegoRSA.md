
## DESCRIPCION
- A message has been encrypted using RSA. The public key is gone… but someone might have been careless with the private key. Can you recover it and decrypt the message? Download the [flag](https://challenge-files.cylabacademy.net/library/cd170c0e341c181c93172139e85c2b00cb4d64184768c43706a6ac8234903dbe/flag.enc) and [image](https://challenge-files.cylabacademy.net/library/cd170c0e341c181c93172139e85c2b00cb4d64184768c43706a6ac8234903dbe/image.jpg).

## SOLUCION
```
- Se descargaron los artefactos provistos por el desafío: `flag.enc` (criptograma de 256 bytes correspondiente a un bloque RSA de 2048 bits) e `image.jpg`.
    
- **Fase de Esteganografía (Extracción de la Clave Privada):**
    
    - Se analizaron los metadatos de la imagen utilizando `exiftool image.jpg`.
        
    - El campo de metadatos `Comment` contenía una cadena hexadecimal extensa que comenzaba con `2d2d2d2d2d424547494e2050524956415445204b4559...`, la cual traduce en texto plano al encabezado `-----BEGIN PRIVATE KEY-----`.
        
    - Se extrajo el valor del comentario y se convirtió de hexadecimal a bytes para regenerar el archivo `private.key`:
        
        Bash
        
        ```
        python3 -c '
        import subprocess
        hex_key = subprocess.check_output(["exiftool", "-s3", "-Comment", "image.jpg"]).decode().strip()
        with open("private.key", "wb") as f:
            f.write(bytes.fromhex(hex_key))
        '
        ```
        
- **Fase de Criptoanálisis (Descifrado Asimétrico RSA):**
    
    - Con la clave privada recuperada en formato PEM, se descifró el archivo `flag.enc` utilizando OpenSSL:
        
        Bash
        
        ```
        openssl pkeyutl -decrypt -inkey private.key -in flag.enc
        ```
        
    - La ejecución procesó el bloque criptográfico y reveló la bandera en texto claro.

academy{rs4_k3y_1n_1mg_42380180}

```

## NOTAS ADICIONALES
Exposición de Claves Criptográficas y Metadatos:

1. **Fuga de Claves Privadas:** La seguridad del esquema asimétrico RSA depende exclusivamente del secreto de la clave privada ($d, p, q$). Al incrustarse dentro de los metadatos de un archivo distribuido públicamente, el esquema pierde toda confidencialidad, reduciendo el ataque a una simple lectura de metadatos (CWE-312 / CWE-522).
    
2. **Campos EXIF/COM en JPEG:** El marcador de comentario `0xFFFE` (COM) en imágenes JPEG permite almacenar texto arbitrario sin alterar la representación visual de la imagen, siendo un vector frecuente en desafíos de esteganografía básica.

## REFERENCIAS

- Reto original: picoCTF 2026 - Categoría: Cryptography (Easy).
    
- Autor: Yahaya Meddy.
    
- Conceptos aplicados: Criptografía Asimétrica RSA, Metadatos EXIF/JPEG, Decodificación Hexadecimal, OpenSSL `pkeyutl`.