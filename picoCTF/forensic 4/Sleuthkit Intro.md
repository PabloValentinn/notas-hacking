
## DESCRIPCION
- Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.

Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

[Download disk image](https://challenge-files.cylabacademy.net/library/d8718cbbc14dcd9f9aad532a51d7a01b00e1715ca3b1d654dfef687d0b15cbf5/disk.img.gz)

## SOLUCION
```
- Se descargó y descomprimió la imagen de disco proporcionada por la plataforma.
    
- Se utilizó la herramienta `mmls`, parte de la suite _The Sleuth Kit_, ejecutando el comando `mmls disk.img` para analizar la estructura del volumen.
    
- El análisis arrojó una tabla de particiones DOS (DOS Partition Table).
    
- Se identificó la partición objetivo en la fila `002` (Slot `000:000`), correspondiente al sistema de archivos `Linux (0x83)`.
    
- Se extrajo el valor numérico de la columna "Length", resultando en una longitud de `0000202752` sectores.
    
- Se estableció una conexión con el servicio de verificación remota de la plataforma mediante la utilidad de red `nc` (Netcat).
    
- Se ingresó el valor de la longitud (202752) en el _prompt_ del servidor remoto, el cual validó la respuesta y retornó la bandera del reto de manera exitosa.

academy{mm15_f7w!}

```
## NOTAS ADICIONALES

- Análisis de Tablas de Particiones: El comando `mmls` de _The Sleuth Kit_ (TSK) es fundamental en la fase de preparación del análisis forense digital. Se utiliza para listar y examinar el diseño lógico de las particiones dentro de un disco o imagen en bruto. Muestra el inicio, fin y longitud de los espacios asignados a sistemas de archivos, así como los espacios no asignados (unallocated) o metadatos. Conocer el sector de inicio (offset) y la longitud exacta de una partición específica es indispensable para poder explorar sus archivos internos posteriormente con otras herramientas forenses como `fls` o extraer su contenido utilizando `icat`.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Forensics (Medium).
    
- Conceptos aplicados: Volume System Analysis, Partition Tables, The Sleuth Kit (`mmls`).