## DESCRIPCION
There's an interesting script in the user's home directory

The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

`Hostname: saturn.picoctf.net Port: 52694 Username: picoplayer Password: password`

## SOLUCION
```
ssh picoplayer@ saturn.picoctf.net -p 52694

The authenticity of host '[saturn.picoctf.net]:52694 ([13.59.203.175]:52694)' can't be established.
ED25519 key fingerprint is SHA256:DiJcS90U9QussLS8HLR6l6BGJb5eCA0vRmA18IvDvw8.
This key is not known by any other names

picoplayer@challenge:~$ man useless

useless
     useless, -- This is a simple calculator script

SYNOPSIS
     useless, [add sub mul div] number1 number2

DESCRIPTION
     Use the useless, macro to make simple calulations
     like addition,subtraction, multiplication and divi-
     sion.

Examples
     ./useless add 1 2
       This will add 1 and 2 and return 3

     ./useless mul 2 3
       This will return 6 as a product of 2 and 3

     ./useless div 6 3
       This will return 2 as a quotient of 6 and 3

     ./useless sub 6 5
       This will return 1 as a remainder of substraction
       of 5 from 6

Authors
     This script was designed and developed by Cylab
     Africa

picoplayer@challenge:~$ cat useless

picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_4151}

```

## NOTAS ADICIONALES
- man te proporciona un manual de ayuda completo de un comando o ejecutable

## REFERENCIAS