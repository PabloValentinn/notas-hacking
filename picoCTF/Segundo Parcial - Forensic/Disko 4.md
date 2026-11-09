
## Descripción

Can you find the flag in this disk image? This time I deleted the file! Let see you get it now! Download the disk image [here](https://challenge-files.cylabacademy.net/library/d11cb680ea12a21fc0d5fdb414a325b8c800bd2fbf4b546df09d428f0e84b4c4/disko-4.dd.gz)

1. How would you look for deleted files?

## Solución

1. Se descargó y descomprimió la imagen de disco:
    ```bash
    gzip -d disko-4.dd.gz
    ```

2. Se buscaron los archivos eliminados utilizando `fls`:
    ```bash
    fls -r disko-4.dd | grep "\*"
    ```
    Se encontraron los siguientes archivos:
    ```text
    + r/r * 522629: messages
    + r/r * 532021: dont-delete.gz
    ```

3. Se recuperó el archivo `dont-delete.gz` mediante su número de inodo `532021`:
    ```bash
    icat disko-4.dd 532021 > dont-delete.gz
    ```

4. Se descomprimió y visualizó el contenido del archivo recuperado:
    ```bash
    gzip -dc dont-delete.gz
    ```
    Se obtuvo el siguiente resultado:
```
academy{d3l_d0n7_h1d3_w3ll_187a1210}
```

## Notas adicionales

- Cuando un archivo es eliminado en sistemas de archivos FAT o ext, los datos del archivo raramente se sobrescriben de forma inmediata; el sistema simplemente marca la entrada en la tabla de asignación como disponible y desvincula el puntero de directorio. Mientras los clusters no sean reutilizados por nuevas escrituras, la recuperación forense de los datos (_file carving_ o recuperación vía metadatos) es trivial.

## Referencias
https://github.com/hackadvisermx/cylab-picoctf