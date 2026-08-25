## RETO

## DESCRIPCION
What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

## SOLUCION
```
Python 3.10.12 (main, Mar  3 2026, 11:56:32) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import base64
>>> base64.b64decode("bDNhcm5fdGgzX3lwcDM1")
b'l3arn_th3_r0p35'
>>> 
picoCTF{l3arn_th3_r0p35}

```

## NOTAS ADICIONALES
Abrir el interprte de python en cylab e importar base 64

## REFERENCIAS
https://es.wikipedia.org/wiki/Base64