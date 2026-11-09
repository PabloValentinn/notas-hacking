## DESCRIPCION
This file has a flag in plain sight (aka "in-the-clear").

## SOLUCION
```
pabloval-academy@webshell:~$ WGET https://challenge-files.picoctf.net/c_wily_courier/a2320fa31ee7a0cd35e9ad6685c56de110bb6cc12e048fc9341a42e9066791c8/flag
-bash: WGET: command not found
pabloval-academy@webshell:~$ wget https://challenge-files.picoctf.net/c_wily_courier/a2320fa31ee7a0cd35e9ad6685c56de110bb6cc12e048fc9341a42e9066791c8/flag
--2026-08-20 05:10:49--  https://challenge-files.picoctf.net/c_wily_courier/a2320fa31ee7a0cd35e9ad6685c56de110bb6cc12e048fc9341a42e9066791c8/flag
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 3.160.5.95, 3.160.5.64, 3.160.5.40, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|3.160.5.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 34 [application/octet-stream]
Saving to: 'flag'

flag           100%[====>]      34  --.-KB/s    in 0s      

2026-08-20 05:10:49 (16.1 MB/s) - 'flag' saved [34/34]

pabloval-academy@webshell:~$ ^C
pabloval-academy@webshell:~$ cat flag
picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}
pabloval-academy@webshell:~$ ^C
pabloval-academy@webshell:~$ 


picoCTF{s4n1ty_v3r1f13d_9b8fa0bc}
```

## NOTAS ADICIONALES
Bajar el archivo de la consola y hacer un cat flag

## REFERENCIAS
[Webshell](https://webshell.cylabacademy.org/)