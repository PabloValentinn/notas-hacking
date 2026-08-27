## DESCRIPCION
- Run the Python script and convert the given number from decimal to binary to get the flag.

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/22/convertme.py
--2026-08-27 01:56:52--  https://artifacts.picoctf.net/c/22/convertme.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.40, 3.160.5.18, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.40|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1189 (1.2K) [application/octet-stream]
Saving to: 'convertme.py'

convertme.py         100%[======================>]   1.16K  --.-KB/s    in 0s      

2026-08-27 01:56:53 (513 MB/s) - 'convertme.py' saved [1189/1189]

pabloval-academy@webshell:~$ python3 convertme.py
If 83 is in decimal base, what is it in binary base?
Answer: 1010011
That is correct! Here's your flag: 


picoCTF{4ll_y0ur_b4535_762f748e}
```

## NOTAS ADICIONALES
- Se descarga con wget y se ejecuta el archivo, el 83 en binario es 1010011

## REFERENCIAS

- https://www.rapidtables.com/convert/number/decimal-to-binary.html?x=83