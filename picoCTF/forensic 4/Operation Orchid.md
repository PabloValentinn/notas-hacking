
## DESCRIPCION
- Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://challenge-files.cylabacademy.net/library/7d645367284f9df9139dd5ad212e5c3bd0815b7674ca700648a3983158394892/disk.flag.img.gz)

## SOLUCION
```
- Se descargó y extrajo la imagen de disco del reto.
    
- Se utilizó la herramienta `mmls` para analizar las particiones, identificando el sector de inicio (_offset_) de la partición principal de Linux en `411648`.
    
- Se realizó una búsqueda recursiva de archivos utilizando el comando `fls -o 411648 disk.flag.img -r | grep flag`. El resultado mostró que el archivo original `flag.txt` (Inode 1876) había sido eliminado, pero se encontró una versión cifrada llamada `flag.txt.enc` en el Inode `1782`.
    
- Se extrajo el archivo cifrado al entorno local ejecutando `icat -o 411648 disk.flag.img 1782 > flag.txt.enc`.
    
- Para descubrir el método de cifrado, se buscó el historial de comandos del usuario del sistema con `fls -o 411648 disk.flag.img -r | grep history`, localizando el archivo `.ash_history` en el Inode `1875`.
    
- Se volcó el contenido del historial utilizando `icat -o 411648 disk.flag.img 1875`. La salida reveló el comando de cifrado exacto: `openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567`, seguido del comando `shred -u flag.txt` que destruyó el archivo original de forma segura.
    
    PNG+ 1
    
- Con esta información, se procedió a aplicar la operación criptográfica inversa en la terminal local ejecutando: `openssl aes256 -d -salt -in flag.txt.enc -k unbreakablepassword1234567`, lo cual descifró exitosamente el archivo y reveló la bandera.


academy{h4un71ng_p457_718ebd29} 
```

## NOTAS ADICIONALES
- Técnicas Anti-Forenses y Artefactos del Sistema: Este desafío introduce el concepto de "Anti-Forensics". El uso de utilidades como `shred` sobrescribe los bloques de datos físicos del archivo original, haciendo que herramientas de recuperación estándar (como extraer el archivo reasignado con `icat`) fallen. Sin embargo, un principio clave del análisis forense es que las acciones suelen dejar múltiples rastros. Al analizar los artefactos del sistema operativo (en este caso, el registro de la _shell_ en `.ash_history`), un investigador puede reconstruir las acciones exactas de un usuario y revertir medidas de ofuscación como el cifrado mediante OpenSSL.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Anti-Forensics (`shred`), Shell History Analysis, File System Browsing (`fls`), Data Extraction (`icat`), OpenSSL Decryption.