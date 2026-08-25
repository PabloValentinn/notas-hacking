## DESCRIPCION
Can you look at the data in this binary? The bash script might help!

## SOLUCION
```
 https://challenge-files.picoctf.net/c_wily_courier/b94bae11002f8fd650a028c91c0e5427b3122a0049c43a3ed483299b8d61665b/static

 https://challenge-files.picoctf.net/c_wily_courier/b94bae11002f8fd650a028c91c0e5427b3122a0049c43a3ed483299b8d61665b/ltdis.sh
 
 pabloval-academy@webshell:~$ chmod +x ltdis.sh
pabloval-academy@webshell:~$ ./ltdis.sh
Attempting disassembly of  ...
objdump: 'a.out': No such file
objdump: section '.text' mentioned in a -j option, but not found in any input file
Disassembly failed!
Usage: ltdis.sh <program-file>
Bye!
pabloval-academy@webshell:~$ ./ltdis.sh static
Attempting disassembly of static ...
Disassembly successful! Available at: static.ltdis.x86_64.txt
Ripping strings from binary with file offsets...
Any strings found in static have been written to static.ltdis.strings.txt with file offset
pabloval-academy@webshell:~$ cat static.ltdis.strings.txt | grep pico
   3020 
   
   picoCTF{d15a5m_t34s3r_20335e41}
```

## NOTAS ADICIONALES
- .sh son archivos que contienen comandos de linux agrupados, se les llama script de bash

## REFERENCIAS
- rm borra todos los archivos en la carpeta actual