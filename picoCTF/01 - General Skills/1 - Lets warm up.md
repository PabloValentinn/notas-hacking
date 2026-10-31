## RETO
- Reto 1
## DESCRIPCION
- If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII?
## SOLUCION
- ir al sitio web rapidtables
 picoCTF{p} 

## NOTAS ADICIONALES
- Siempre tener en cuenta el formato
## SOLUCION 2
abrir el interprete de pytho en cylab 
convertir 0x70 a int
```
Python 3.10.12 (main, Mar  3 2026, 11:56:32) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> int(0x70)
112
>>> chr(112)
'p'
>>> 
```

## REFERENCIAS
- [Hex a ASCII | Convertidor de cadena hexadecimal a texto](https://www.rapidtables.org/convert/number/hex-to-ascii.html)