

## DESCRIPCION
 - Download this disk image and find the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://challenge-files.cylabacademy.net/library/162bc8bf6dd1abbc5269c16570e170277369a39cf46bdd8d99443e136fabcc5f/disk.flag.img.gz)

## SOLUCION
```
- Se descargó el archivo comprimido del reto y se extrajo la imagen de disco `disk.flag.img` utilizando utilidades de descompresión (como `gunzip`).
    
- Se ejecutó `mmls disk.flag.img` para analizar la tabla de particiones, identificando la partición principal de Linux (Linux 0x83) en el sector de inicio (offset) `360448`.
    
- Se utilizó el comando `fls -o 360448 disk.flag.img` para listar los archivos y directorios de la partición, navegando por la estructura del sistema de archivos a través de los números de Inode asignados a cada directorio.
    
- Tras inspeccionar los directorios clave (como `/root` o `/home`), se localizó el archivo objetivo que contenía la bandera, el cual estaba asociado al Inode número `2371`.
    
- Se ejecutó el comando `icat -o 360448 -r disk.flag.img 2371` para leer los bloques de datos correspondientes a ese Inode, extrayendo e imprimiendo exitosamente el texto de la bandera directamente en la terminal.

academy{by73_5urf3r_85e9b307}

```
## NOTAS ADICIONALES
- Navegación de Sistemas de Archivos y Extracción por Inodes: Este reto consolida el flujo de trabajo forense integral con The Sleuth Kit (TSK). Mientras que `mmls` identifica la estructura a nivel de volumen, `fls` permite inspeccionar la jerarquía interna del sistema de archivos sin necesidad de montar la imagen en el sistema operativo anfitrión, previniendo alteraciones accidentales de la evidencia. Finalmente, `icat` interactúa de forma directa con los metadatos estructurales (Inodes) para volcar los datos crudos de un archivo. Esta metodología permite a los analistas recuperar información intacta e incluso extraer archivos que el sistema operativo ha marcado como eliminados.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Partition Analysis (`mmls`), File System Browsing (`fls`), Data Extraction (`icat`), Inode Navigation.