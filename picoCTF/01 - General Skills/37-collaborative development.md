## DESCRIPCION
- My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?

You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/179/challenge.zip)

## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c_titan/179/challenge.zip
--2026-08-29 21:59:26--  https://artifacts.picoctf.net/c_titan/179/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.95, 3.160.5.18, 3.160.5.40, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 24648 (24K) [application/octet-stream]
Saving to: 'challenge.zip.1'

challenge.zip.1      100%[===================>]  24.07K  --.-KB/s    in 0.01s   

2026-08-29 21:59:26 (2.24 MB/s) - 'challenge.zip.1' saved [24648/24648]

pabloval-academy@webshell:~$ unzip challenge.zip
Archive:  challenge.zip

pabloval-academy@webshell:~$ cd drop-in
pabloval-academy@webshell:~/drop-in$ 

pabloval-academy@webshell:~$ cd drop-in
pabloval-academy@webshell:~/drop-in$ git branch -a

[2]+  Stopped                 git branch -a
pabloval-academy@webshell:~/drop-in$ git checkout feature/part-1
Switched to branch 'feature/part-1'
pabloval-academy@webshell:~/drop-in$ git branch -a

[3]+  Stopped                 git branch -a
pabloval-academy@webshell:~/drop-in$ git branch -a
        

pabloval-academy@webshell:~/drop-in$ git checkout feature/part-1
Already on 'feature/part-1'

pabloval-academy@webshell:~/drop-in$ cat flag.py
print("Printing the flag...")
print("picoCTF{t3@mw0rk_", end='')pabloval-academy@webshell:~/drop-in$ 

Switched to branch 'feature/part-2'
pabloval-academy@webshell:~/drop-in$ cat flag.py
print("Printing the flag...")

print("m@k3s_th3_dr3@m_", end='')pabloval-academy@webshell:~/drop-in$ 

pabloval-academy@webshell:~/drop-in$ git checkout feature/part-3
Switched to branch 'feature/part-3'
pabloval-academy@webshell:~/drop-in$ cat flag.py
print("Printing the flag...")

print("w0rk_798f9981}")
pabloval-academy@webshell:~/drop-in$ 

picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_798f9981}



```

## NOTAS ADICIONALES
- Se uso el comando `git checkout` para saltar entre tres ramas de desarrollo distintas y se leyo el archivo `flag.py` en cada una.

## REFERENCIAS
- Gemini IA