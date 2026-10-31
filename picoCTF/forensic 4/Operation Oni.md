
## DESCRIPCION

- Download this disk image, find the key and log into the remote machine.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download disk image](https://challenge-files.cylabacademy.net/library/32b4f7450d7368e22562f75fed35fecd7bdfa2172559a90a42a149e27d781464/disk.img.gz)
- Remote machine: `ssh -i key_file -p 15924 ctf-player@chatelaine.cylabacademy.net`

## SOLUCION
```
- Se descargó y descomprimió la imagen de disco del reto.
    
- Se analizó la estructura del disco utilizando los comandos `fdisk -l disk.img` y `file disk.img` en lugar de `mmls`. Esto permitió identificar que la partición principal de Linux comenzaba en el sector de inicio (_offset_) `206848`.
    
- Se realizó una búsqueda recursiva de archivos relacionados con SSH ejecutando `fls -o 206848 disk.img -r | grep ssh`. Entre los resultados, se identificó el directorio oculto `.ssh` correspondiente al Inode `3916`.
    
- Se inspeccionó el contenido de dicho directorio con `fls -o 206848 disk.img 3916`, localizando la clave privada SSH `id_ed25519` en el Inode `2345`.
    
- Se extrajo la clave privada al entorno local utilizando el comando `icat -o 206848 disk.img 2345 > key_file`.
    
- Para cumplir con los estrictos requisitos de seguridad del protocolo SSH, se restringieron los permisos del archivo de la clave ejecutando `chmod 600 key_file`.
    
- Finalmente, se estableció una conexión segura con el servidor remoto utilizando el comando proporcionado por la plataforma actualizada: `ssh -i key_file -p 17706 ctf-player@xebec.cylabacademy.net`. Una vez dentro del servidor Ubuntu, se leyó el archivo de la bandera.
 
```

## NOTAS ADICIONALES
- Análisis de Artefactos de Red y Alternativas de Herramientas: Este desafío resalta dos puntos clave en la respuesta a incidentes y el análisis forense. Primero, demuestra que existen múltiples utilidades nativas en Linux (como `fdisk` y `file`) para inspeccionar tablas de particiones y metadatos de volumen cuando las herramientas especializadas de _The Sleuth Kit_ no son la única opción. Segundo, subraya la importancia de revisar los directorios `.ssh` de los usuarios; la extracción de claves privadas (como `id_rsa` o `id_ed25519`) es una táctica crítica tanto para auditores de seguridad como para atacantes que buscan realizar movimientos laterales hacia otras máquinas en una red.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Partition Analysis (`fdisk`, `file`), File System Browsing (`fls`), Data Extraction (`icat`), SSH Key Authentication, File Permissions (`chmod`).