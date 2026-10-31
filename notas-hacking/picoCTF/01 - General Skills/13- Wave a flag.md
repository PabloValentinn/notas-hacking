## DESCRIPCION
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

This program will only work in the webshell or another Linux computer.

To get the file accessible in your shell, enter the following in the Terminal prompt: $ wget url here where the url can be found in the details section.



## SOLUCION
```
pabloval-academy@webshell:~$ wget  https://challenge-files.picoctf.net/c_wily_courier/5a478d0b24d6a4f4185e3adb7a78c41cdad626fb02fe80e083dc33bf8b197d3d/warm
--2026-08-24 16:43:38--  https://challenge-files.picoctf.net/c_wily_courier/5a478d0b24d6a4f4185e3adb7a78c41cdad626fb02fe80e083dc33bf8b197d3d/warm


abloval-academy@webshell:~$ file warm
warm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=9e46ec8729d2f2aa8ffc4b1cdc058081bddcfe67, for GNU/Linux 3.2.0, with debug_info, not stripped
pabloval-academy@webshell:~$ 

for GNU/Linux 3.2.0, with debug_info, not stripped
pabloval-academy@webshell:~$ chmod +x warm
pabloval-academy@webshell:~$ ./warm
Hello user! Pass me a -h to learn what I can do!
pabloval-academy@webshell:~$ ./warm -h

picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

## NOTAS ADICIONALES
- Descargamos el archivo y verificamos que tipo de archivo es, como es ejecutable le damos permiso de ejecucion chmod+x
- ./warm ejecuta el binario warm una vez que ya tiene los permisos de ejecucion
- file permite saber de que tipo es un archivo
- ELF es el formato de archivo ejecutable linux(equivalente al exe de windows)

## REFERENCIAS
Chatgpt
