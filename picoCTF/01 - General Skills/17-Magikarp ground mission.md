## DESCRIPCION
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin.

## SOLUCION
```
pabloval-academy@webshell:~$ ssh -p 57473 ctf-player@wily-courier.picoctf.net
The authenticity of host '[wily-courier.picoctf.net]:57473 ([18.189.99.27]:57473)' can't be established.
ED25519 key fingerprint is SHA256:ErlUUvYlrAxfSW1tIdzfOnGTBSr5OFkZvz0nMN4Vodw.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:3: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[wily-courier.picoctf.net]:57473' (ED25519) to the list of known hosts.
ctf-player@wily-courier.picoctf.net's password: 
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 6.17.0-1013-aws x86_64)

ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt

ctf-player@pico-chall$ cat^C
ctf-player@pico-chall$ cat 1of3.flag.txt
picoCTF{xxsh_

ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  etc                       media  run   usr
bin            home                      mnt    sbin  var
boot           instructions-to-3of3.txt  opt    srv
challenge      lib                       proc   sys
dev            lib64                     root   tmp
ctf-player@pico-chall$ cat 2of3.flag.txt
0ut_0f_//4t3r_
ctf-player@pico-chall$ 

ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt
0b24fc4f}ctf-player@pico-chall$ 


picoCTF{xxsh_0ut_0f_//4t3r_0b24fc4f}
```

## NOTAS ADICIONALES
Se debe acceder a archivo por archivo usando cd, luego con ls se ven que archivos hay para que con cat nos de el contenido del archivo

## REFERENCIAS
Webshell
