
## DESCRIPCION
- A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server? Access the server using `nc xebec.cylabacademy.net 29555`

## SOLUCION
```
- Se analizó la consigna del reto, la cual describe un servidor corporativo comprometido debido al almacenamiento de contraseñas mediante funciones criptográficas de dispersión (_hashing_) débiles y sin protección adicional.
    
- Se estableció comunicación con el servicio remoto a través del puerto interactivo asignado:
    
    Bash
    
    ```
    nc xebec.cylabacademy.net 29555
    ```
    
- El servicio solicitó de forma secuencial la reversión de tres hashes de contraseñas comunes (ataques basados en diccionario / tablas de pre-cómputo):
    
    1. **Primer Hash (MD5):**
        
        - Hash entregado: `482c811da5d5b4bc6d497ffa98491e38` (32 caracteres hexadecimales / 128 bits).
            
        - Se identificó como una suma de verificación MD5 correspondiente a una contraseña genérica de lista de uso frecuente.
            
        - Contraseña en texto plano: `password123`.
            
    2. **Segundo Hash (SHA-1):**
        
        - Hash entregado: `b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3` (40 caracteres hexadecimales / 160 bits).
            
        - Identificado como un resumen criptográfico de la familia Secure Hash Algorithm 1 (SHA-1).
            
        - Contraseña en texto plano: `letmein`.
            
    3. **Tercer Hash (SHA-256):**
        
        - Hash entregado: `916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745` (64 caracteres hexadecimales / 256 bits).
            
        - Se procesó contra diccionarios estándar (`rockyou.txt`) y servicios de búsqueda reversa en bases de datos de pre-cómputo (_lookup tables_ como CrackStation).
            
        - Contraseña en texto plano: `qwerty098`.
            
- Tras ingresar correctamente cada una de las contraseñas en la secuencia interactiva del servidor, este validó la coincidencia de los tres resúmenes e imprimió la bandera del reto.


academy{UseStr0nG_h@shEs_&PaSswDs!_35c6b1f4}
```

## NOTAS ADICIONALES
- Inseguridad de Algoritmos de Hash Rápidos y Ausencia de Sal (_Salting_):

1. **Funciones de propósito general vs. Hash de contraseñas:** Algoritmos como MD5, SHA-1 y SHA-256 fueron diseñados para comprobar integridad de datos con alta velocidad de cómputo. Utilizarlos directamente para almacenar contraseñas es una mala práctica crítica, ya que un atacante puede calcular miles de millones de intentos por segundo mediante GPU/ASIC o consultar tablas de pre-cómputo masivas (_rainbow tables_ y bases de datos indexadas).
    
2. **Mitigación adecuada:** Para el resguardo seguro de credenciales se deben implementar funciones de derivación de claves deliberadamente costosas en cómputo y memoria (_memory-hard_ / _slow hashing_), tales como **Argon2id**, **bcrypt** o **scrypt**, siempre acompañadas de una sal criptográfica (_salt_) única, aleatoria y de longitud suficiente por cada usuario para neutralizar ataques basados en diccionarios globales precalculados.

## REFERENCIAS
- Reto original: picoCTF 2025 - Categoría: Cryptography (Easy).
    
- Conceptos aplicados: Criptoanálisis de Hashes Débiles, Ataques de Diccionario, Tablas de Pre-cómputo, Identificación de Funciones Criptográficas (MD5, SHA-1, SHA-256).