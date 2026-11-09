
## Descripción

Can you find the flag in this disk image? Wrap what you find in the academy{} flag format. Download the disk image [here](https://challenge-files.cylabacademy.net/library/0b369ed5974a5e777ca3bc323bd39d75a6f27762a449d16cd2a0ffc08b2a6aa8/timeline-1-partition4.img.gz)

1. Create a Sleuthkit MAC timeline!
2. Look at recent timestamps
3. Pay close attention to timestamps near an anti-forensic action
4. Filter only new files by grepping for `macb`
## Solución

1. Se descomprimió la imagen de disco y se renombró:
    ```bash
    gzip -d timeline-1-partition4.img.gz
    mv timeline-1-partition4.img timeline1.img
    ```

2. Se generó una línea de tiempo mediante The Sleuth Kit:
    ```bash
    fls -r -m / timeline1.img > body.txt
    mactime -b body.txt -d > mactime.csv
    ```

3. Se filtraron los archivos con marcas temporales `macb` para identificar actividad reciente:
    ```bash
    grep "macb" mactime.csv | tail -n 10
    ```
    Se identificó el archivo `/etc/chat`, creado el 1 de diciembre de 2025, con inodo `32716`.

4. Se extrajo el contenido del archivo utilizando su inodo:
    ```bash
    icat timeline1.img 32716
    ```
    Se obtuvo la siguiente cadena codificada:
    ```text
    NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK
    ```

5. Se decodificó la cadena mediante Base64:
    ```bash
    echo "NTczNDE3aDEzcl83aDRuXzdoM18xNDU3XzU4NTI3YmIyMjIK" | base64 -d
    ```
    Se recuperó el mensaje utilizado para construir la bandera.

```
academy{573417h13r_7h4n_7h3_1457_58527bb222}
```

## Notas adicionales

- En respuesta a incidentes, la correlación temporal entre eventos de administración (comandos en historiales como `.bash_history` o `.ash_history`), artefactos creados temporalmente y el apagado forzado del equipo permite reconstruir la ventana exacta de actividad del intruso.
## Referencias