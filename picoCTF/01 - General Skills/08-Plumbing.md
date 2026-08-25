## DESCRIPCION
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?

Connect to fickle-tempest.picoctf.net 64353.

## SOLUCION
```
pabloval-academy@webshell:~$ nc fickle-tempest.picoctf.net 64353 | grep "picoCTF{"
picoCTF{digital_plumb3r_1eBfC512}
^C


picoCTF{digital_plumb3r_1eBfC512}
```

## NOTAS ADICIONALES
Nos conectamos al servidor desde la consola y todo lo que el servidor mande de respuesta lo colocamos en una archivo en este caso H, ya solo con cat y grep buscamos la bandera

## REFERENCIAS
[Webshell](https://webshell.cylabacademy.org/)