## DESCRIPCION
Can you make sense of this file?

## SOLUCION
```
pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/477/enc_flag
--2026-08-25 03:23:47--  https://artifacts.picoctf.net/c/477/enc_flag
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.40, 3.160.5.95, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.

pabloval-academy@webshell:~$ ls
Addadshashanammu.zip  file.1    static.ltdis.strings.txt
README.txt            flag      static.ltdis.x86_64.txt
enc_flag              ltdis.sh  strings
file                  static    warm
pabloval-academy@webshell:~$ cat enc_flag | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d


picoCTF{base64_n3st3d_dic0d!n8_d0wnl04d3d_de523f49}
```

## NOTAS ADICIONALES
Linux tiene una herramienta nativa para esto llamada `base64`. El parámetro `-d` le indica que decodifique (_decode_).

## REFERENCIAS
Chatgpt