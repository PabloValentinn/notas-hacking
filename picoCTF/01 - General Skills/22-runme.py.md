## DESCRIPCION
- Run the `runme.py` script to get the flag. Download the script with your browser or with `wget` in the webshell.

## SOLUCION
```
pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/34/runme.py
--2026-08-26 23:25:48--  https://artifacts.picoctf.net/c/34/runme.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.95, 3.160.5.18, 3.160.5.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 270 [application/octet-stream]
Saving to: 'runme.py'

runme.py             100%[======================>]     270  --.-KB/s    in 0s      

2026-08-26 23:25:48 (158 MB/s) - 'runme.py' saved [270/270]

pabloval-academy@webshell:~$ ls
Addadshashanammu.zip  enc_flag  files.zip  static                    warm
README.txt            file      flag       static.ltdis.strings.txt
big-zip-files         file.1    ltdis.sh   static.ltdis.x86_64.txt
big-zip-files.zip     files     runme.py   strings
pabloval-academy@webshell:~$ cat runme.py
#!/usr/bin/python3
################################################################################
# Python script which just prints the flag
################################################################################

flag ='picoCTF{run_s4n1ty_run}'
print(flag)

picoCTF{run_s4n1ty_run}
```

## NOTAS ADICIONALES
- Se usa el wget y el cat
## REFERENCIAS
Webshell

