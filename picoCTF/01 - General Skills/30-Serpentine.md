## DESCRIPCION
- Find the flag in the Python script!

[Download Python script](https://artifacts.picoctf.net/c/37/serpentine.py)

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/37/serpentine.py
--2026-08-27 04:35:29--  https://artifacts.picoctf.net/c/37/serpentine.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.40, 3.160.5.18, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2550 (2.5K) [application/octet-stream]
Saving to: 'serpentine.py'

serpentine.py        100%[======================>]   2.49K  --.-KB/s    in 0s      

2026-08-27 04:35:29 (947 MB/s) - 'serpentine.py' saved [2550/2550]

pabloval-academy@webshell:~$ nano serpentine.py
pabloval-academy@webshell:~$ python serpentine.py

    Y
  .-^-.
 /     \      .- ~ ~ -.
()     ()    /   _ _   `.                     _ _ _
 \_   _/    /  /     \   \                . ~  _ _  ~ .
   | |     /  /       \   \             .' .~       ~-. `.
   | |    /  /         )   )           /  /             `.`.
   \ \_ _/  /         /   /           /  /                `'
    \_ _ _.'         /   /           (  (
                    /   /             \  \
                   /   /               \  \
                  /   /                 )  )
                 (   (                 /  /
                  `.  `.             .'  /
                    `.   ~ - - - - ~   .'
                       ~ . _ _ _ _ . ~

Welcome to the serpentine encourager!


a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) b
picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}
a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) ^CTraceback (most recent call last):
  File "/home/pabloval-academy/serpentine.py", line 80, in <module>
    main()
  File "/home/pabloval-academy/serpentine.py", line 63, in main
    choice = input('What would you like to do? (a/b/c) ')
KeyboardInterrupt

picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}
```

## NOTAS ADICIONALES
- Se ingreso con nano al archivo y se reacomodo la funcion que estaba mal

## REFERENCIAS
Webshell
