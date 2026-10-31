## DESCRIPCION
- Unzip this archive and find the flag.
## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/503/big-zip-files.zip
--2026-08-25 04:12:02--  https://artifacts.picoctf.net/c/503/big-zip-files.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.40, 3.160.5.18, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.40|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3182988 (3.0M) [application/octet-stream]
Saving to: 'big-zip-files.zip'

unzip big-zip-files.zip

grep -r "picoCTF{" .

picoCTF{gr3p_15_m4g1c_ef8790dc}
```

## NOTAS ADICIONALES

se usa el comando `unzip` para extraer todo su contenido:

## REFERENCIAS
Chatgpt