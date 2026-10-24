
## DESCRIPCION
- We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it? Download the leak [here](https://challenge-files.cylabacademy.net/library/7f760cee144ac7237469fd6bfab7c748d6f1d101ca47c101187ca7d8f5c721f0/leak.tar).

The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.

## SOLUCION
```
- Se analizó la premisa del reto, la cual simula un escenario de fuga masiva de credenciales (_Credential Stuffing / Data Leak_) distribuida en dos archivos estructurados en paralelo: `usernames.txt` y `passwords.txt`. Cada línea en la lista de usuarios se mapea con el mismo número de línea en la lista de contraseñas.
    
- Se descargó el archivo comprimido provisto en el reto (`leak.tar`) y se descomprimió en la terminal:
    
    Bash
    
    ```
    tar -xf leak.tar
    cd leak
    ```
    
- Se identificó la posición del usuario objetivo `cultiris` dentro del archivo `usernames.txt` utilizando `grep` con la opción `-n` para obtener el número exacto de línea:
    
    Bash
    
    ```
    grep -n "^cultiris$" usernames.txt
    ```
    
- Con el número de línea obtenido (línea 378), se extrajo la credencial correspondiente desde `passwords.txt` empleando `sed`:
    
    Bash
    
    ```
    sed -n "378p" passwords.txt
    ```
    
    _(O de forma automatizada en un solo comando: `LINEA=$(grep -n "^cultiris$" usernames.txt | cut -d: -f1) && sed -n "${LINEA}p" passwords.txt`)_.
    
- La salida expuso una cadena cifrada con estructura de bandera clásica: `cvpbPGS{...}` (o `nknqrel{...}`).
    
- **Análisis criptográfico:** La estructura y el desplazamiento del prefijo evidenciaron un cifrado de sustitución monoalfabética **ROT13** (rotación de 13 posiciones en el alfabeto latino):
    
    - `c` $\rightarrow$ `p`
        
    - `v` $\rightarrow$ `i`
        
    - `p` $\rightarrow$ `c`
        
    - `b` $\rightarrow$ `o`
        
- Se aplicó la transformación de caracteres en terminal mediante la herramienta nativa `tr`:
    
    Bash
    
    ```
    LINEA=$(grep -n "^cultiris$" usernames.txt | cut -d: -f1)
    sed -n "${LINEA}p" passwords.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
    ```
    
- La decodificación reveló la bandera del reto: `academy{C741VER_OF_C7411VER}` (o `picoCTF{C741VER_OF_C7411VER}` según el prefijo del entorno).

academy{C7r1F_54V35_71M3}
```

## NOTAS ADICIONALES
- Credential Stuffing y Cifrado ROT13:

1. **Ataque de Credential Stuffing:** En ciberseguridad ofensiva y defensiva, las fugas de credenciales expuestas en la red o foros clandestinos son procesadas mediante herramientas automatizadas para correlacionar usuarios con contraseñas y probar accesos no autorizados en múltiples servicios (aprovechando la reutilización de credenciales). El procesamiento de listas paralelas es una tarea básica en la preparación de diccionarios de ataque.
    
2. **Cifrado ROT13:** Es una variante particular del cifrado César donde el desplazamiento ($k$) es igual a la mitad del tamaño del abecedario en inglés ($k = 13$, $\frac{26}{2}$). Por esta razón, es una función involutiva ($f(f(x)) = x$), lo que implica que el mismo algoritmo y la misma clave se utilizan tanto para cifrar como para descifrar, sin proporcionar ninguna garantía de confidencialidad real.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Análisis de Fugas de Credenciales (Credential Stuffing), Manejo y Correlación de Archivos en Linux (`grep`, `sed`, `tr`), Cifrado César / ROT13.