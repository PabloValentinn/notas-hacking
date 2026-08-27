## DESCRIPCION
- Fix the syntax error in this Python script to print the flag.

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/25/fixme1.py
--2026-08-27 02:15:34--  https://artifacts.picoctf.net/c/25/fixme1.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.18, 3.160.5.40, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.18|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 837 [application/octet-stream]
Saving to: 'fixme1.py'

fixme1.py            100%[======================>]     837  --.-KB/s    in 0s      

2026-08-27 02:15:35 (323 MB/s) - 'fixme1.py' saved [837/837]

pabloval-academy@webshell:~$ nano fixme1.py
pabloval-academy@webshell:~$ nano fixme1.py
pabloval-academy@webshell:~$ python3 fixme1.py
That is correct! Here's your flag:


 picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```

## NOTAS ADICIONALES
- Se descarga el archivo con wget y con nano podemos modificar el archivo

## REFERENCIAS
Gemini
