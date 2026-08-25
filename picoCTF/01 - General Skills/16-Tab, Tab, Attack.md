## DESCRIPCION
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames.

## SOLUCION 1
```

 https://challenge-files.picoctf.net/c_wily_courier/1d211441eced2214a10b0c2aacbf05d153aafcd6edc055f913cafcdb48a0b02b/Addadshashanammu.zip
 
 pabloval-academy@webshell:~$ strings Addadshashanammu.zip | grep pico
printf("*ZAP!* 

picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}\n");
pabloval-academy@webshell:~$ 
```

## NOTAS ADICIONALES
control A va al inicio de la linea
control E va al final
## REFERENCIAS
cd Enter me lleva directo a la carpeta del usuario
cd ~ hace lo mimsmo que el anterior

echo $HOME me dice cual es la carpeta del usuario

