
## DESCRIPCION

- BookShelf Pico, my premium online book-reading service.

I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!

## SOLUCION
```
- Se accedió a la aplicación web proporcionada por el reto, iniciando sesión con las credenciales básicas proporcionadas (`user` / `user`). Se observó que la aplicación utilizaba tokens JWT (JSON Web Tokens) para gestionar la autenticación y autorización de los usuarios.
    
- Se inspeccionó el código fuente de la aplicación (descargado desde el enlace proporcionado en el reto). Se analizó el archivo `JwtService.java`, el cual contenía la lógica de generación y validación de tokens. Se identificó que la clave secreta utilizada para firmar los tokens se generaba mediante la clase `SecretGenerator.java`.
    
- Al inspeccionar `SecretGenerator.java`, se descubrió que la función `generateRandomString` contenía una clave secreta codificada de forma estática: `return "1234";`. Aunque el código intentaba leer una clave desde un archivo externo (`server_secret.txt`), en ausencia de este, utilizaba la clave débil predefinida.
    
- Se procedió a capturar el token JWT original asignado al usuario `user`. Utilizando las herramientas de desarrollador del navegador (F12) > pestaña **Application** > **Local Storage**, se localizó la clave `auth-token` que contenía el token de sesión.
    
- Se decodificó el token original (utilizando herramientas como [jwt.io](https://jwt.io/) o scripts en Python) para inspeccionar su estructura. El payload del token contenía los campos: `role: "Free"`, `userId: 1`, `email: "user"`.
    
- Se procedió a falsificar el token para elevar privilegios. Se modificó el payload para que contuviera los valores de un usuario administrador:
    
    - `"role": "Admin"`
        
    - `"userId": 2`
        
    - `"email": "admin"`
        
- Se firmó el nuevo token utilizando la clave secreta descubierta en el código fuente: `1234`. El algoritmo de firma utilizado fue HS256.
    
- Se inyectó el nuevo token falsificado en el navegador, reemplazando el valor de la clave `auth-token` en el Local Storage. Adicionalmente, se actualizó la clave `token-payload` con los nuevos valores para evitar conflictos en el frontend.
    
- Se recargó la página. El servidor validó el token firmado con la clave `1234` y otorgó acceso con privilegios de administrador. Se pudo visualizar y acceder al libro "Flag" en la estantería, obteniendo así la bandera del reto.
    
- La bandera obtenida fue: `picoCTF{w34k_jwt_n0t_g00d_7745dc02}`.

```

## NOTAS ADICIONALES

- - **JSON Web Token (JWT) y Claves Débiles:** Los JWT son un estándar para transmitir información de forma segura entre partes. Sin embargo, si la clave secreta utilizada para firmar los tokens es débil o predecible (como `"1234"`), un atacante puede falsificar tokens válidos. Esto se conoce como **JWT Forgery** o **Weak Secret Key Vulnerability**.
    
- **Elevación de Privilegios mediante Manipulación de Tokens:** Al modificar el campo `role` en el payload del JWT, un atacante puede escalar privilegios de un usuario normal (`Free`) a un administrador (`Admin`). Si el servidor confía ciegamente en el rol declarado en el token sin validarlo contra una base de datos, la aplicación queda comprometida.
    
- **Importancia de la Validación en el Servidor:** La validación de los tokens JWT debe realizarse siempre en el servidor. El servidor debe verificar la firma del token y, además, validar que los datos contenidos en el payload (como el rol) correspondan a la realidad del usuario en la base de datos. No se debe confiar únicamente en la información proporcionada por el cliente.
    
- **Prevención:** Para prevenir este tipo de vulnerabilidades, se deben utilizar claves secretas fuertes y aleatorias (generadas criptográficamente). Además, se debe implementar una validación estricta de los tokens en el servidor, verificando la firma y los permisos del usuario en cada petición.

## REFERENCIAS
- - Reto original: picoCTF 2023 - Categoría: Web Exploitation (Java Code Analysis!?!).
    
- Conceptos aplicados: JWT Forgery, Weak Secret Key, Privilege Escalation, Source Code Analysis, Local Storage Manipulation.