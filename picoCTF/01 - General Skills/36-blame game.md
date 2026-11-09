## DESCRIPCION
- Someone's commits seems to be preventing the program from working. Who is it?

You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/157/challenge.zip)

## SOLUCION
```

pabloval-academy@webshell:~/drop-in$ wget https://artifacts.picoctf.net/c_titan/157/challenge.zip

pabloval-academy@webshell:~/drop-in$ unzip challenge.zip

pabloval-academy@webshell:~/drop-in$ git log | grep "picoCTF"

picoCTF{@sk_th3_1nt3rn_cfca95b2}
```

## NOTAS ADICIONALES
- `git log` junto con el comando `grep` para filtrar todo el historial del repositorio buscando específicamente el texto "picoCTF".

## REFERENCIAS
Gemini