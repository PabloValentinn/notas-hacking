

## DESCRIPCION
- Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility.

The source code for the training vault is here: [VaultDoorTraining.java](https://challenge-files.cylabacademy.net/library/83cc2880b948e8f4ec4aead98be96ed71b1e83e3525bddac26f4e1030fc740f7/VaultDoorTraining.java)

## SOLUCION
```

- Se analizó la consigna del reto, el cual introduce la categoría de ingeniería inversa orientada al análisis estático de código fuente en Java.
    
- Se descargó el archivo fuente `VaultDoorTraining.java` mediante el enlace provisto en la plataforma.
    
- Se inspeccionó el archivo desde la terminal para examinar la lógica de autenticación:
    
    Bash
    
    ```
    cat VaultDoorTraining.java
    ```
    
- **Análisis Estático del Código:**
    
    - El método principal `main` solicita al usuario una cadena de texto, extrae el contenido interior descartando el envoltorio del formato (`substring`) y lo envía como argumento al método de validación `checkPassword`:
        
        Java
        
        ```
        public boolean checkPassword(String password) {
            return password.equals("w4rmup_m3m0r135_8ed8573a");
        }
        ```
        
    - Se constató que no existe ningún algoritmo de hashing, cifrado ni ofuscación de flujo; la verificación se realiza mediante una comparación directa contra una cadena constante incrustada en texto plano (_hardcoded string_).
        
- Se extrajo el valor literal mediante herramientas de filtrado de texto:
    
    Bash
    
    ```
    grep -o 'password.equals("[^"]*")' VaultDoorTraining.java
    ```
    
- Se encapsuló la clave recuperada dentro del formato formal de entrega: `academy{w4rmup_m3m0r135_8ed8573a}` (o `picoCTF{w4rmup_m3m0r135_8ed8573a}`).
```

## NOTAS ADICIONALES
- Inseguridad por Credenciales Embebidas (_Hardcoded Credentials_):

1. **Riesgo de Seguridad:** La presencia de secretos, tokens o contraseñas en texto claro dentro del código fuente es una debilidad crítica (catalogada comúnmente bajo CWE-798: _Use of Hard-coded Credentials_). Al compilar o distribuir el binario, cualquier usuario con acceso al artefacto puede extraer la clave mediante inspección directa o descompilación del bytecode.
    
2. **Buenas Prácticas:** La verificación de accesos o credenciales debe realizarse siempre comparando valores con funciones de dispersión criptográfica seguras y lentas (como Argon2 o bcrypt), evitando almacenar claves en claro tanto en el cliente como en el repositorio de código.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Easy).
    
- Autor: Mark E. Haase.
    
- Conceptos aplicados: Análisis Estático de Código Fuente, Inspección de Código Java, CWE-798 (Credenciales Embebidas).