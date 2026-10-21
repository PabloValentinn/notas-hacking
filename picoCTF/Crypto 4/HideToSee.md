
## DESCRIPCION
- How about some hide and seek heh? Look at this image [here](https://challenge-files.cylabacademy.net/library/d1a6b6365f32679d90a52e42234c7bad12bdfb9ac5e87598af9f1202ee047227/atbash.jpg).

## SOLUCION
```- Se analizó la consigna del reto, cuyo título (_HideToSee_) y descripción aludían a la técnica de esteganografía mediante la herramienta `steghide`.
    
- Se descargó el archivo multimedia adjunto denominado `atbash.jpg`.
    
- Se utilizó la herramienta `steghide` para inspeccionar y extraer posibles flujos de datos ocultos incrustados en los coeficientes DCT del archivo JPEG:
    
    Bash
    
    ```
    steghide extract -sf atbash.jpg -p ""
    ```
    
    _(El parámetro `-p ""` especifica una contraseña vacía/en blanco, evitando errores de autenticación interactiva)_.
    
- La extracción generó con éxito el archivo de texto plano `encrypted.txt`.
    
- Al inspeccionar su contenido con `cat encrypted.txt`, se observó una cadena de texto ofuscada con un formato de bandera análogo a `krxlXGU{zgyzhs_xizxp_...}`.
    
- **Criptoanálisis:** El propio nombre del archivo original (`atbash.jpg`) indicaba el algoritmo empleado: el **Cifrado Atbash**, un cifrado de sustitución monoalfabética donde el abecedario se invierte de forma simétrica ($A \leftrightarrow Z$, $B \leftrightarrow Y$, etc.).
    
- Se ejecutó un script en una sola línea de Python para sustituir los caracteres alfabéticos por su versión invertida preservando mayúsculas, minúsculas, números y caracteres especiales:
    
    Bash
    
    ```
    python3 -c '
    import string
    text = open("encrypted.txt").read()
    normal = string.ascii_lowercase + string.ascii_uppercase
    atbash = string.ascii_lowercase[::-1] + string.ascii_uppercase[::-1]
    table = str.maketrans(normal, atbash)
    print(text.translate(table).strip())
    '
    ```
    
- El proceso descifró el texto, revelando la bandera correspondiente al reto: `academy{atbash_crack_...}` (o `picoCTF{atbash_crack_...}` según la variante de la plataforma).


## NOTAS ADICIONALES
- Esteganografía con Steghide y Cifrado Clásico Atbash: Este reto implementa el principio de defensa en profundidad inversa (o seguridad por oscuridad estratificada), combinando un contenedor esteganográfico para ocultar la existencia del canal de comunicación y un cifrado clásico para proteger el contenido en caso de extracción. `steghide` opera reemplazando pseudorandomicamente bits en archivos de audio e imágenes sin alterar perceptiblemente su apariencia gráfica o acústica. Una vez extraído, el cifrado Atbash (originario del hebreo antiguo) no ofrece resistencia criptográfica moderna, ya que carece de clave secreta y su espacio de búsqueda es unitario e involutivo ($f(f(x)) = x$).

## REFERENCIAS
- Reto original: picoCTF 2023 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Esteganografía en JPEG (`steghide`), Cifrado Atbash, Sustitución Monoalfabética Involutiva, Python One-Liners.

