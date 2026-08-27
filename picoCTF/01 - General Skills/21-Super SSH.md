## DESCRIPCION
Using a Secure Shell (SSH) is going to be pretty important.

## SOLUCION
```
pabloval-academy@webshell:~$ ssh ctf-player@titan.picoctf.net -p 50225
The authenticity of host '[titan.picoctf.net]:50225 ([3.139.174.234]:50225)' can't be established.
ED25519 key fingerprint is SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:6: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:50225' (ED25519) to the list of known hosts.
ctf-player@titan.picoctf.net's password: 
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_5d09a462}
Connection to titan.picoctf.net closed.

picoCTF{s3cur3_c0nn3ct10n_5d09a462}
```

## NOTAS ADICIONALES
- Se conecta al servidor usan ssh

## REFERENCIAS
webshell

