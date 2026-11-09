


# DESCRIPCION
- Python scripts are invoked kind of like programs in the Terminal... Can you run `ende.py` using `password.txt` to get `flag.txt.en`?

## SOLUCION
```

- Se descargaron los tres archivos proporcionados por la plataforma del reto (`ende.py`, `password.txt` y `flag.txt.en`) en un entorno local basado en Linux.
    
- Se utilizó el comando de lectura estándar `cat password.txt` en la terminal para visualizar el contenido del archivo y se copió la contraseña en texto plano al portapapeles.
    
- Se analizó la sintaxis de ejecución del script y se procedió a invocar el intérprete de Python en la línea de comandos, pasando la bandera de descifrado (`-d`) junto con el archivo objetivo, utilizando el comando: `python3 ende.py -d flag.txt.en`.
    
- Durante la ejecución del script, el programa hizo una pausa interactiva solicitando la clave de acceso. Se pegó la contraseña obtenida en el primer paso.
    
- Tras validar correctamente la clave, el script de Python aplicó la rutina de descifrado sobre el archivo y proyectó la bandera de manera exitosa en la salida estándar (consola).
```

## NOTAS ADICIONALES
- Interacción con la CLI (Línea de Comandos): Este reto sirve como una demostración práctica de cómo los scripts desarrollados en Python interactúan con el sistema operativo Linux. Se ilustra el uso de paso de argumentos (como `-d` para definir el comportamiento de descifrado) a través de librerías nativas como `sys.argv` o `argparse`. Cifrado Simétrico: El script `ende.py` (cuyo nombre deriva de _encrypt/decrypt_) emplea un modelo de criptografía simétrica. Esto significa que la misma clave estática y secreta almacenada en `password.txt` es el único mecanismo utilizado tanto para cifrar la información original como para recuperar el texto plano.
## REFERENCIAS

- - Reto original: picoCTF 2021 - Categoría: General Skills (Python Wrangling).
    
- Documentación de herramientas: Invocación básica del intérprete de Python (`python3`) y manual del comando `cat` en sistemas operativos GNU/Linux.