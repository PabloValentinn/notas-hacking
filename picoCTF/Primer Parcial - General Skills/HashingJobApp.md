

# DESCRIPCION

- If you want to hash with the best, beat this test! `nc xebec.cylabacademy.net 33561`
## SOLUCION

- Se estableció conexión con el servidor del reto a través de la terminal utilizando la herramienta Netcat (`nc xebec.cylabacademy.net 33561`).
    
- Al inicializar la conexión, el programa interactivo proporcionó una cadena de texto específica entre comillas y solicitó calcular su hash MD5 antes de que se agotara un límite de tiempo muy corto.
    
- Se abrió una segunda pestaña en la terminal de Linux para poder realizar el cálculo sin interrumpir ni cerrar la conexión activa de Netcat.
    
- Se utilizó el comando `echo -n 'cadena_proporcionada' | md5sum` en la segunda terminal para generar el hash. Se aplicó estrictamente la bandera `-n` en el comando `echo` para evitar que la terminal añadiera un salto de línea invisible (`\n`), lo cual habría alterado drásticamente el resultado matemático del hash.
    
- Se copió el hash MD5 resultante (una cadena de 32 caracteres hexadecimales), se regresó a la primera terminal y se envió la respuesta al servidor.
    
- Se repitió este proceso manual de lectura, cálculo y envío de forma rápida y precisa durante las pruebas consecutivas que exigió el sistema.
    
- Al enviar todos los hashes correctos dentro del tiempo límite establecido, el servidor validó el éxito de la tarea e imprimió la bandera en la salida estándar de la consola.
## NOTAS ADICIONALES

- Funciones Hash (Hashing): Un hash es un algoritmo matemático unidireccional que transforma cualquier bloque de datos en una serie de caracteres con una longitud fija. El algoritmo MD5, utilizado en este reto, siempre devuelve 32 caracteres. Aunque hoy en día MD5 se considera obsoleto y vulnerable para almacenar contraseñas reales, sigue siendo ampliamente utilizado en CTFs y verificaciones de integridad de archivos. Precisión en comandos de consola (El problema del salto de línea): Un error extremadamente común al resolver este tipo de retos manualmente en Linux es omitir la bandera `-n` en el comando `echo`. Dado que el hash cambia por completo si se altera un solo bit de la entrada, agregar un espacio o un "Enter" accidental al final de la palabra hace que el servidor rechace inmediatamente la respuesta.

## REFERENCIAS

- - Reto original: Beginner picoMini 2022 - Categoría: General Skills (HashingJobApp).
    
- Documentación de herramientas: Manual de los comandos `md5sum` y `echo` en sistemas operativos basados en Linux/Unix.