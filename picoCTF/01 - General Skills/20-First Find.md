## DESCRIPCION
Unzip this archive and find the file named 'uber-secret.txt'

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/500/files.zip
--2026-08-25 04:35:07--  https://artifacts.picoctf.net/c/500/files.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.18, 3.160.5.95, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.18|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3995553 (3.8M) [application/octet-stream]
Saving to: 'files.zip'

unzip files.zip

find . -name "uber-secret.txt"

pabloval-academy@webshell:~$ find . -name "uber-secret.txt"
./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
pabloval-academy@webshell:~$ ^C
pabloval-academy@webshell:~$ cat ./files/adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
picoCTF{f1nd_15_f457_ab443fd1}

picoCTF{f1nd_15_f457_ab443fd1}
```

## NOTAS ADICIONALES
El comando `find` devolverá la ruta exacta donde está escondido el archivo

## REFERENCIAS
https://www.ionos.com/digitalguide/server/configuration/linux-find-command/