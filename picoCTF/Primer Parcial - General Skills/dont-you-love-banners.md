
## DESCRIPCION
- Can you abuse the banner? The server has been leaking some crucial information on `xebec.cylabacademy.net 48462`. Use the leaked information to get to the server.

To connect to the running application use `nc xebec.cylabacademy.net 35491`. From the above information abuse the machine and find the flag in the /root directory.

## SOLUCION
```

- Se inició la instancia del reto y se obtuvieron los puertos de conexión.
    
- Utilizando la herramienta `nc` (Netcat), se realizó la conexión al puerto 48462 para extraer la información "filtrada" (leaked), obteniendo la contraseña: `My_Passw@rd_@1234`.
    
- Posteriormente, se estableció conexión al puerto de la aplicación principal (35491) e ingresó la contraseña obtenida.
    
- El servidor presentó un cuestionario de validación de conocimientos de ciberseguridad, el cual se resolvió respondiendo:
    
    - **Conferencia:** `DEF CON`
        
    - **Primer hacker (Phreaking):** `John Draper`
        
- Al superar la validación, se obtuvo acceso a una consola (shell) interactiva con los privilegios del usuario estándar (`player`).
    
- Mediante el comando `ls -la`, se inspeccionaron los permisos del directorio actual, descubriendo que el archivo `banner` (el cual contiene el texto de bienvenida que el servidor lee al iniciar conexión) pertenecía al usuario `player`, permitiendo su modificación.
    
- Se ejecutó el abuso de escalada de privilegios eliminando el archivo original y creando un enlace simbólico (symlink) hacia la bandera del administrador:
    
    - `rm banner`
        
    - `ln -s /root/flag.txt banner`
        
- Se interrumpió la conexión actual (`Ctrl+C`) y se realizó una nueva conexión al servidor mediante Netcat (`nc xebec.cylabacademy.net 35491`).
    
- Al iniciar la nueva sesión, el servidor ejecutó la lectura del archivo "banner" con permisos elevados, imprimiendo en pantalla el contenido de `/root/flag.txt` en lugar del mensaje de bienvenida, revelando así la flag.
```

## NOTAS ADICIONALES
- - **Vulnerabilidad de Symlink (Enlace Simbólico):** Este reto ilustra una vulnerabilidad lógica común donde una aplicación con altos privilegios (en este caso, el proceso que imprime el banner de bienvenida) confía ciegamente en un archivo controlado por un usuario con menores privilegios. Al reemplazar el archivo por un acceso directo a un recurso protegido, el atacante engaña al sistema para que exponga información confidencial.
    
- **Herramienta Netcat (`nc`):** Conocida como "la navaja suiza" de las redes, fue fundamental para establecer las conexiones TCP crudas necesarias tanto para capturar la contraseña filtrada como para interactuar con la consola de la aplicación.

## REFERENCIAS
- - Reto original: **picoCTF 2024** - Categoría: _General Skills_ (dont-you-love-banners).
    
- Documentación de Linux sobre gestión de enlaces simbólicos (`man ln`).
    
- Conceptos de escalada de privilegios locales en entornos Unix/Linux.