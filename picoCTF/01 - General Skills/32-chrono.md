## DESCRIPCION
- How to automate tasks to run at intervals on linux servers?

Use ssh to connect to this server:

`Server: saturn.picoctf.net Port: 54165 Username: picoplayer Password: bLgSMmbY6X`

## SOLUCION
```

pabloval-academy@webshell:~$ ssh -p 54165 picoplayer@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:54165 ([13.59.203.175]:54165)' can't be established.
ED25519 key fingerprint is SHA256:dMTscRrUiURy7uMu5eGWwEKdd2FzqLzx6LfWhssWnNQ.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:54165' (ED25519) to the list of known hosts.
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

picoplayer@challenge:~$ cat /etc/crontab
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_1b4d8744}
picoplayer@challenge:~$ ^C
picoplayer@challenge:~$ Connection to saturn.picoctf.net closed by remote host.
Connection to saturn.picoctf.net closed.

picoCTF{Sch3DUL7NG_T45K3_L1NUX_1b4d8744}
```

## NOTAS ADICIONALES
- En Linux, este sistema se llama **cron**, por lo que la solución lógica era revisar su archivo principal de configuración (`crontab`), donde el administrador escondió el texto del reto.

## REFERENCIAS
Gemini IA
