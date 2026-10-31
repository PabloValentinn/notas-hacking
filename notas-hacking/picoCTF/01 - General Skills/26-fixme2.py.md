## DESCRIPCION
Fix the syntax error in the Python script to print the flag.

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/6/fixme2.py
--2026-08-27 02:33:45--  https://artifacts.picoctf.net/c/6/fixme2.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.40, 3.160.5.18, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1029 (1.0K) [application/octet-stream]
Saving to: 'fixme2.py'

fixme2.py            100%[======================>]   1.00K  --.-KB/s    in 0s      

2026-08-27 02:33:45 (159 MB/s) - 'fixme2.py' saved [1029/1029]

pabloval-academy@webshell:~$ nano fixme2.py
pabloval-academy@webshell:~$ python fixme2.py
That is correct! Here's your flag: 


picoCTF{3qu4l1ty_n0t_4551gnm3nt_f6a5aefc}
```

## NOTAS ADICIONALES
- En python se debe usar un == para comparar

## REFERENCIAS
webshell
