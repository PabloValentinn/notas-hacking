## DESCRIPCION

What was I last working on? I remember writing a note to help me remember...

You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/68/challenge.zip)

## SOLUCION

```

pabloval-academy@webshell:~$ wget https://artifacts.picoctf.net/c_titan/68/challenge.zip
--2026-08-29 05:23:48--  https://artifacts.picoctf.net/c_titan/68/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.95, 3.160.5.64, 3.160.5.18, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17738 (17K) [application/octet-stream]
Saving to: 'challenge.zip'

challenge.zip        100%[===================>]  17.32K  --.-KB/s    in 0.007s  

2026-08-29 05:23:48 (2.53 MB/s) - 'challenge.zip' saved [17738/17738]

pabloval-academy@webshell:~$ unzip challenge.zip
Archive:  challenge.zip
replace drop-in/message.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/message.txt     
replace drop-in/.git/description? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/description  
replace drop-in/.git/hooks/applypatch-msg.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
replace drop-in/.git/hooks/commit-msg.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/commit-msg.sample  
replace drop-in/.git/hooks/fsmonitor-watchman.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sample  
replace drop-in/.git/hooks/post-update.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/post-update.sample  
replace drop-in/.git/hooks/pre-applypatch.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/pre-applypatch.sample  
replace drop-in/.git/hooks/pre-commit.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: yes
  inflating: drop-in/.git/hooks/pre-commit.sample  
replace drop-in/.git/hooks/pre-merge-commit.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/pre-merge-commit.sample  
replace drop-in/.git/hooks/pre-push.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/pre-push.sample  
replace drop-in/.git/hooks/pre-rebase.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/pre-rebase.sample  
replace drop-in/.git/hooks/pre-receive.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/pre-receive.sample  
replace drop-in/.git/hooks/prepare-commit-msg.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/prepare-commit-msg.sample  
replace drop-in/.git/hooks/update.sample? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/hooks/update.sample  
replace drop-in/.git/info/exclude? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/info/exclude  
replace drop-in/.git/refs/heads/master? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
 extracting: drop-in/.git/refs/heads/master  
replace drop-in/.git/HEAD? [y]es, [n]o, [A]ll, [N]one, [r]ename: yy
 extracting: drop-in/.git/HEAD       
replace drop-in/.git/config? [y]es, [n]o, [A]ll, [N]one, [r]ename: 
error:  invalid response [{ENTER}]
replace drop-in/.git/config? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/config     
   creating: drop-in/.git/objects/43/
 extracting: drop-in/.git/objects/43/246218ab4fc7b30e9a9dff073e012316851469  
   creating: drop-in/.git/objects/25/
 extracting: drop-in/.git/objects/25/16effb8d70e33bdd0023629b164a77225e1ec2  
   creating: drop-in/.git/objects/70/
 extracting: drop-in/.git/objects/70/5ff639b7846418603a3272ab54536e01e3dc43  
replace drop-in/.git/index? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: drop-in/.git/index      
replace drop-in/.git/COMMIT_EDITMSG? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
 extracting: drop-in/.git/COMMIT_EDITMSG  
replace drop-in/.git/logs/HEAD? [y]es, [n]o, [A]ll, [N]one, [r]ename: ^Cpabloval-nge.zip@webshell:~$ wget https://artifacts.picoctf.net/c_titan/68/challen
--2026-08-29 05:24:34--  https://artifacts.picoctf.net/c_titan/68/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.160.5.64, 3.160.5.18, 3.160.5.40, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.160.5.64|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 17738 (17K) [application/octet-stream]
Saving to: 'challenge.zip.1'

challenge.zip.1      100%[===================>]  17.32K  --.-KB/s    in 0.007s  

2026-08-29 05:24:34 (2.51 MB/s) - 'challenge.zip.1' saved [17738/17738]

pabloval-academy@webshell:~$ unzip challenge.zip
Archive:  challenge.zip
replace drop-in/message.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: A
  inflating: drop-in/message.txt     
  inflating: drop-in/.git/description  
  inflating: drop-in/.git/hooks/applypatch-msg.sample  
  inflating: drop-in/.git/hooks/commit-msg.sample  
  inflating: drop-in/.git/hooks/fsmonitor-watchman.sample  
  inflating: drop-in/.git/hooks/post-update.sample  
  inflating: drop-in/.git/hooks/pre-applypatch.sample  
  inflating: drop-in/.git/hooks/pre-commit.sample  
  inflating: drop-in/.git/hooks/pre-merge-commit.sample  
  inflating: drop-in/.git/hooks/pre-push.sample  
  inflating: drop-in/.git/hooks/pre-rebase.sample  
  inflating: drop-in/.git/hooks/pre-receive.sample  
  inflating: drop-in/.git/hooks/prepare-commit-msg.sample  
  inflating: drop-in/.git/hooks/update.sample  
  inflating: drop-in/.git/info/exclude  
 extracting: drop-in/.git/refs/heads/master  
 extracting: drop-in/.git/HEAD       
  inflating: drop-in/.git/config     
 extracting: drop-in/.git/objects/43/246218ab4fc7b30e9a9dff073e012316851469  
 extracting: drop-in/.git/objects/25/16effb8d70e33bdd0023629b164a77225e1ec2  
 extracting: drop-in/.git/objects/70/5ff639b7846418603a3272ab54536e01e3dc43  
  inflating: drop-in/.git/index      
 extracting: drop-in/.git/COMMIT_EDITMSG  
  inflating: drop-in/.git/logs/HEAD  
  inflating: drop-in/.git/logs/refs/heads/master  
pabloval-academy@webshell:~$ cd drop-in
pabloval-academy@webshell:~/drop-in$ git log

[1]+  Stopped                 git log


 picoCTF{t1m3m@ch1n3_b476ca06}
```

## NOTAS ADICIONALES
- `git log` para leer el historial de versiones.

## REFERENCIAS
- Gemini
