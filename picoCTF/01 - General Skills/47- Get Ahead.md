## DESCRIPCION
- Find the flag being held on this server to get ahead of the competition

## SOLUCION
``` 

[warning] /usr/bin/burpsuite: No JAVA_CMD set for run_java, falling back to JAVA_CMD = java
                                                                             
┌──(kali㉿kali)-[~]
└─$ curl s -s ^[[200~view-source:wily-courier.picoctf.net:52495/index.php  
zsh: bad pattern: ^[[200~view-source:wily-courier.picoctf.net:52495/index.php
                                                                             
┌──(kali㉿kali)-[~]
└─$ curl -s -X view-source:wily-courier.picoctf.net:52495/index.php?     
curl: (2) no URL specified
curl: try 'curl --help' or 'curl --manual' for more information
                                                                             
┌──(kali㉿kali)-[~]
└─$ curl -s ^[[200~http://wily-courier.picoctf.net:52495/index.php?~
zsh: bad pattern: ^[[200~http://wily-courier.picoctf.net:52495/index.php?~
                                                                             
┌──(kali㉿kali)-[~]
└─$ curl -s http://wily-courier.picoctf.net:52495/index.php?        

<!doctype html>
<html>
<head>
    <title>Red</title>
    <link rel="stylesheet" type="text/css" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
        <style>body {background-color: red;}</style>
</head>
        <body>
                <div class="container">
                        <div class="row">
                                <div class="col-md-6">
                                        <div class="panel panel-primary" style="margin-top:50px">
                                                <div class="panel-heading">
                                                        <h3 class="panel-title" style="color:red">Red</h3>
                                                </div>
                                                <div class="panel-body">
                                                        <form action="index.php" method="GET">
                                                                <input type="submit" value="Choose Red"/>
                                                        </form>
                                                </div>
                                        </div>
                                </div>
                                <div class="col-md-6">
                                        <div class="panel panel-primary" style="margin-top:50px">
                                                <div class="panel-heading">
                                                        <h3 class="panel-title" style="color:blue">Blue</h3>
                                                </div>
                                                <div class="panel-body">
                                                        <form action="index.php" method="POST">
                                                                <input type="submit" value="Choose Blue"/>
                                                        </form>
                                                </div>
                                        </div>
                                </div>
                        </div>
                </div>
        </body>
</html>
                                                                             
┌──(kali㉿kali)-[~]
└─$ curl -s s -I  http://wily-courier.picoctf.net:52495/index.php?
HTTP/1.1 200 OK
Date: Mon, 07 Sep 2026 16:24:12 GMT
Server: Apache/2.4.38 (Debian)
X-Powered-By: PHP/7.2.34
flag: picoCTF{r3j3ct_th3_du4l1ty_8b13f07}
Content-Type: text/html; charset=UTF-8


picoCTF{r3j3ct_th3_du4l1ty_8b13f07}
```

## NOTAS ADICIONALES
- Fui a la pagina y le di a inspeccionar, despues me fui a network y recargue la pagina, en la lista de elementos de red que aparecieron,  clic derecho sobre el primero (el documento principal). Selecciona **Copiar** > **Copiar como fetch**. Luego se va a la pestaña de consola, pego el codigo que copie y busco el GET que lo cambio por HEAD

## REFERENCIAS
Gemini IA
