## DESCRIPCION
- Can you crack the password to get the flag?

Download the password checker [here](https://artifacts.picoctf.net/c/16/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/16/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/16/level3.hash.bin) in the same directory too.

There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.
## SOLUCION
```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.py
--2026-08-27 04:23:22--  https://artifacts.picoctf.net/c/16/level3.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.40, 3.160.5.18, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1337 (1.3K) [application/octet-stream]
Saving to: 'level3.py'

level3.py            100%[======================>]   1.31K  --.-KB/s    in 0s      

2026-08-27 04:23:22 (62.4 MB/s) - 'level3.py' saved [1337/1337]

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.flag.txt.enc
--2026-08-27 04:23:59--  https://artifacts.picoctf.net/c/16/level3.flag.txt.enc
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.18, 3.160.5.40, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 31 [application/octet-stream]
Saving to: 'level3.flag.txt.enc'

level3.flag.txt.enc  100%[======================>]      31  --.-KB/s    in 0s      

2026-08-27 04:23:59 (1.88 MB/s) - 'level3.flag.txt.enc' saved [31/31]


pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c/16/level3.hash.bin
--2026-08-27 04:24:34--  https://artifacts.picoctf.net/c/16/level3.hash.bin
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.95, 3.160.5.18, 3.160.5.40, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16 [application/octet-stream]
Saving to: 'level3.hash.bin'

level3.hash.bin      100%[======================>]      16  --.-KB/s    in 0s      

2026-08-27 04:24:34 (8.66 MB/s) - 'level3.hash.bin' saved [16/16]


pabloval-academy@webshell:~$ cat level3.py
import hashlib

### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_3_pw_check()


# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]

pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: 6997
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: 3ac8
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: f0ac
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: 4b17
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: ec27
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: 4e66
That password is incorrect
pabloval-academy@webshell:~$ python level3.py
Please enter correct password for flag: 865e
Welcome back... your flag, user:


picoCTF{m45h_fl1ng1ng_2b072a90}


pabloval-academy@webshell:~$ ^C
```

## NOTAS ADICIONALES
- Se puso contraseña por contraseña hasta dar con la correcta

## REFERENCIAS
Webshell

