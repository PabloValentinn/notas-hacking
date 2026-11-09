## DESCRIPCION
- Who doesn't love cookies? Try to figure out the best one.

## SOLUCION
```

┌──(kali㉿kali)-[~]
└─$ curl -s http://wily-courier.picoctf.net:50676/check -H  'Cookie: name=10'
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Cookies</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation"><a href="/reset" class="btn btn-link pull-right">Home</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Cookies</h3>
        </div>
        
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
        
        <div class="alert alert-success alert-dismissible" role="alert" id="myAlert">
          <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <!-- <strong>Title</strong> --> That is a cookie! Not very special though...
            </div>
      
      
      
        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>I love biscotti cookies!</b></p>
        </div>


        <footer class="footer">
            <p>&copy; PicoCTF</p>
        </footer>

    </div>
    <script>
    $(document).ready(function(){
        $(".close").click(function(){
            $("myAlert").alert("close");
        });
    });
    </script>
</body>

</html>           


┌──(kali㉿kali)-[~]
└─$ for i in {1..20}; do curl -s http://wily-courier.picoctf.net:50676/check -H  'Cookie: name=$i' | grep "I love"
for> 
for> 
for> 
for> 
for> 12
for> 2
for> 16
for> 
for> 2
                                                                             
┌──(kali㉿kali)-[~]
└─$ for i in {1..20}; do curl -s http://wily-courier.picoctf.net:50676/check -H  'Cookie: name=$i' | grep "I love" done 
for> 
for> 
                                                                             
┌──(kali㉿kali)-[~]
└─$ 
                                                                             
┌──(kali㉿kali)-[~]
└─$ ^[[200~for i in {1..25}; do
zsh: parse error near `do'
                                                                             
┌──(kali㉿kali)-[~]
└─$     curl -s http://wily-courier.picoctf.net:50676/check -b "name=$i" | grep "picoCTF{"
                                                                             
┌──(kali㉿kali)-[~]
└─$ for i in {1..20} do curl -s http://wily-courier.picoctf.net:50676/check -H "name=$i" | grep "picoCTF{"
zsh: parse error near `|'
                                                                             
┌──(kali㉿kali)-[~]
└─$ for i in {1..20} do curl -s http://wily-courier.picoctf.net:50676/check -H "Cookie:name=$i" | grep "picoCTF{"
zsh: parse error near `|'
                                                                             
┌──(kali㉿kali)-[~]
└─$ for i in {1..20} do curl -s http://wily-courier.picoctf.net:50676/check -H "Cookie:name=$i" | grep "picoCTF{"; done 
zsh: parse error near `|'
                                                                             
┌──(kali㉿kali)-[~]
└─$ for i in {1..20};  do curl -s http://wily-courier.picoctf.net:50676/check -H "Cookie:name=$i" | grep "picoCTF{"; done 










            <p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}
            
            
            picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}

```


## NOTAS ADICIONALES

- Entre a la pagina e ingrese a mi extension de cookies, recargue y al ver que no sabia cual era, puse un comando en la terminal for i in {1..20};  do curl -s http://wily-courier.picoctf.net:50676/check -H "Cookie:name=$i" | grep "picoCTF{"; done 

## REFERENCIAS
- Gemini IA