## DESCRIPCION
- Run the Python script `code.py` in the same directory as `codebook.txt`.

- [Download code.py](https://artifacts.picoctf.net/c/2/code.py)
- [Download codebook.txt](https://artifacts.picoctf.net/c/2/codebook.txt)

## SOLUCION
```
pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/2/code.py
--2026-08-27 00:28:30--  https://artifacts.picoctf.net/c/2/code.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.18, 3.160.5.40, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.18|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1278 (1.2K) [application/octet-stream]
Saving to: 'code.py'

code.py              100%[======================>]   1.25K  --.-KB/s    in 0s      

2026-08-27 00:28:30 (522 MB/s) - 'code.py' saved [1278/1278]

pabloval-academy@webshell:~$ ls
README.txt     code.py  file.1  files.zip  ltdis.sh  static   warm
big-zip-files  file     files   flag       runme.py  strings
pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/2/codebook.txt
--2026-08-27 00:28:59--  https://artifacts.picoctf.net/c/2/codebook.txt
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.40, 3.160.5.95, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 27 [application/octet-stream]
Saving to: 'codebook.txt'

codebook.txt         100%[======================>]      27  --.-KB/s    in 0s      

2026-08-27 00:28:59 (11.3 MB/s) - 'codebook.txt' saved [27/27]

pabloval-academy@webshell:~$ python3 code.py
picoCTF{c0d3b00k_455157_7d102d7a}
pabloval-academy@webshell:~$ ^C


picoCTF{c0d3b00k_455157_7d102d7a}

```

## NOTAS ADICIONALES
- Se descargaron los dos archivos para encontrar la bandera porque juntos van de la mano

## REFERENCIAS
Gemini
