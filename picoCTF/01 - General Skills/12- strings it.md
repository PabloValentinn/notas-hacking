## DESCRIPCION
Can you find the flag in [file](https://challenge-files.picoctf.net/c_fickle_tempest/53c039e64942b1c4334781c4987ba7e2ba54f0b2bf39f52c65f3a65dfcbf4194/strings) without running it?

## SOLUCION
```
abloval-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_fickle_tempest/53c039e64942b1c4334781c4987ba7e2ba54f0b2bf39f52c65f3a65dfcbf4194/strings
--2026-08-24 16:35:21--  https://challenge-files.picoctf.net/c_fickle_tempest/53c039e64942b1c4334781c4987ba7e2ba54f0b2bf39f52c65f3a65dfcbf4194/strings


esolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 3.160.5.40, 3.160.5.18, 3.160.5.95, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|3.160.5.40|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 784424 (766K) [application/octet-stream]
Saving to: 'strings'

strings        100%[====>] 766.04K  1.85MB/s    in 0.4s    

2026-08-24 16:35:21 (1.85 MB/s) - 'strings' saved [784424/784424]

pabloval-academy@webshell:~$ chmod +x strings

pabloval-academy@webshell:~$ strings strings | grep pico
picoCTF{5tRIng5_1T_A1b9ECAa}
```

## NOTAS ADICIONALES
- strings: muestra las cadenas (caracteres imprimibles) en un archivo binario(no texto)

## REFERENCIAS