
## DESCRIPCION
-  How about we take you on an adventure on exploring certificate signing requests Take a look at this CSR file [here](https://challenge-files.cylabacademy.net/library/adc86ad64fdfdb57ccdc30281c4c93aa2a8a913259426681737dc7e69d257275/readmycert.csr).
## SOLUCION
```

- Se analizó la descripción del desafío, la cual introduce el concepto de solicitudes de firma de certificados (_Certificate Signing Requests_ o CSR), estructuradas bajo el estándar PKCS#10 y comúnmente codificadas en formato PEM (Base64 delimitado por cabeceras `-----BEGIN CERTIFICATE REQUEST-----`).
    
- Se descargó el archivo provisto denominado `readmycert.csr`.
    
- Al inspeccionar el archivo inicialmente con `cat readmycert.csr`, se identificó el bloque de texto codificado en Base64 representativo de una CSR estándar.
    
- Para parsear y decodificar la estructura ASN.1 del certificado sin requerir herramientas externas ni servicios web, se ejecutó la utilidad de línea de comandos de OpenSSL especializada en gestión de solicitudes (`req`):
    
    Bash
    
    ```
    openssl req -in readmycert.csr -noout -text
    ```
    
    - `-in readmycert.csr`: Especifica la ruta del archivo de entrada.
        
    - `-noout`: Suprime la re-emisión del bloque binario/PEM codificado.
        
    - `-text`: Fuerza la decodificación completa de todos los atributos, extensiones y campos del sujeto en formato legible por humanos.
        
- En la salida devuelta por OpenSSL, se examinó el campo del sujeto (_Subject Distinguished Name_), específicamente el atributo de Nombre Común (_Common Name_ / CN), donde los creadores del reto incrustaron el texto plano:
    
    Plaintext
    
    ```
    Subject: C = US, ST = ..., O = ..., CN = academy{read_mycert_...}
    ```
    
- Alternativamente, se pudo extraer directamente filtrando por la etiqueta del formato con `grep`:
    
    Bash
    
    ```
    openssl req -in readmycert.csr -noout -text | grep -iE "(academy|picoCTF)\{"
    ```
    
- La extracción expuso la bandera del reto: `academy{read_mycert_...}` (o `picoCTF{read_mycert_...}` según la plataforma).
```

## NOTAS ADICIONALES
- Infraestructura de Clave Pública (PKI) y CSR: Una CSR es el mensaje que un solicitante envía a una Autoridad Certificadora (CA) para solicitar la emisión de un certificado digital de identidad (X.509). La solicitud contiene principalmente la clave pública del solicitante, los datos de identificación (_Subject_: país, provincia, organización, dominio/CN) y la firma digital creada con la clave privada correspondiente para demostrar posesión de la misma. A diferencia de un certificado emitido, una CSR no está firmada por una CA de confianza, sino autofirmada por el solicitante, sirviendo como plantilla para la generación del certificado final.
## REFERENCIAS
- Reto original: picoCTF 2023 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Public Key Infrastructure (PKI), Certificate Signing Request (CSR / PKCS#10), Codificación ASN.1 / PEM, Manejo de OpenSSL (`openssl req`).