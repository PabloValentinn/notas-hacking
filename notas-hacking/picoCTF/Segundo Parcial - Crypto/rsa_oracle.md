

## DESCRIPCION
- An attacker was able to intercept communications between a bank and a fintech company. They managed to get the [message](https://challenge-files.cylabacademy.net/library/f0397680c3aded57020481e88d04d8849fa29a48a8150a23c851942cd67f8389/secret.enc) (ciphertext) and the [password](https://challenge-files.cylabacademy.net/library/f0397680c3aded57020481e88d04d8849fa29a48a8150a23c851942cd67f8389/password.enc) that was used to encrypt the message. After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here `nc xebec.cylabacademy.net 30591`. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.

## SOLUCION
```

- Se descargaron e inspeccionaron los archivos `password.enc` y `secret.enc`.
    
- **Criptoanálisis (RSA Blinding / Ataque de Cifrado Elegido):**
    
    - Dado que el oráculo rechaza descifrar directamente el archivo `password.enc`, se aprovechó la propiedad homomórfica (maleabilidad) de RSA.
        
    - Se multiplicó el criptograma original por $2^e$ (donde $e = 65537$) para generar un criptograma alterado que el oráculo descifró sin restricciones.
        
    - Al dividir el texto claro devuelto por 2, se recuperó la contraseña original: `4263a`.
        
- **Descifrado del Archivo:**
    
    - Se utilizó la herramienta OpenSSL con el algoritmo AES-256-CBC y la contraseña extraída para descifrar `secret.enc`:
        
        Bash
        
        ```
        openssl enc -aes-256-cbc -d -in secret.enc -pass pass:4263a
        ```
        
- **Bandera:** Obtenida mediante el texto plano resultante del descifrado de OpenSSL.
```

## NOTAS ADICIONALES
- **Maleabilidad de RSA (CWE-321):** El cifrado RSA sin esquemas de relleno apropiados (como OAEP) permite que un atacante modifique un criptograma y obtenga una relación matemática predecible en el texto claro resultante, invalidando la confidencialidad si se dispone de un oráculo de descifrado activo.

## REFERENCIAS

- Reto original: picoCTF 2024 - Categoría: Cryptography (Medium).
    
- Autor: Geoffrey Njogu.
    
- Conceptos aplicados: RSA Blinding, Cifrado Homomórfico, Criptoanálisis de Oráculos, Descifrado Simétrico AES-256-CBC.