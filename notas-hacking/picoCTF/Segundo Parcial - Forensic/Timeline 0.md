

## Descripción

Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/bf9a20c350075c5863371e078daee1d570d4062902edc8a4a042e02a7cebf161/partition4.img.gz)

1. Create a Sleuthkit MAC timeline!
2. Sloppy timestomping can yield strange (very old) timestamps

## Solución

1. Se descomprimió la imagen de disco:
    ```bash
    gzip -d partition4.img.gz
    ```

2. Se generó un archivo con los metadatos mediante The Sleuth Kit:
    ```bash
    fls -r -m / partition4.img > body.txt
    ```

3. Se analizó la línea de tiempo para encontrar fechas anómalas:
    ```bash
    mactime -b body.txt -d | head -n 10
    ```
    Se encontró el archivo `/bin/bcab` con fecha de 1985 e inodo `4945`.

4. Se extrajo el contenido del archivo mediante su inodo:
    ```bash
    icat partition4.img 4945
    ```
    Se obtuvo una cadena codificada en Base64.

5. Se decodificó la cadena para recuperar la bandera:
    ```bash
    echo "NzFtMzExbjNfMHU3MTEzcl9oM3JfNDNhMmU3YWYK" | base64 -d
    ```

```
academy{71m311n3_0u7113r_h3r_43a2e7af}
```
## Notas adicionales

- El _timestomping_ es una técnica antiforense utilizada por adversarios para camuflar binarios maliciosos o herramientas de ataque asignándoles marcas temporales antiguas o idénticas a las de archivos legítimos del sistema. Sin embargo, inconsistencias entre timestamps de metadatos (como divergencias entre `$STANDARD_INFORMATION` y `$FILE_NAME` en NTFS, o fechas anteriores a la creación del propio sistema operativo) a menudo exponen el artefacto.
## Referencias
https://github.com/hackadvisermx/cylab-picoctf
