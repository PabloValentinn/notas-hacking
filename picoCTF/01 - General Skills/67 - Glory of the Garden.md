
## DESCRIPCION
- This file contains more than it seems. Get the flag from [garden.jpg](https://challenge-files.cylabacademy.net/library/3c60c5a7f7a8067606c51d4b4b3c7913fae709b11e2f2c7adbc0a0b4cda452ff/garden.jpg).
## SOLUCION
```

──(kali㉿kali)-[~]
└─$ wget https://challenge-files.cylabacademy.net/library/3c60c5a7f7a8067606c51d4b4b3c7913fae709b11e2f2c7adbc0a0b4cda452ff/garden.jpg 
--2026-09-28 12:31:07--  https://challenge-files.cylabacademy.net/library/3c60c5a7f7a8067606c51d4b4b3c7913fae709b11e2f2c7adbc0a0b4cda452ff/garden.jpg
Resolving challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)... 13.226.187.66, 13.226.187.40, 13.226.187.37, ...
Connecting to challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)|13.226.187.66|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2295191 (2.2M) [application/octet-stream]
Saving to: ‘garden.jpg’

garden.jpg          100%[================>]   2.19M  1.49MB/s    in 1.5s    

2026-09-28 12:31:09 (1.49 MB/s) - ‘garden.jpg’ saved [2295191/2295191]

                                                                             
┌──(kali㉿kali)-[~]
└─$ srings -n 10 garden.jpg 
Command 'srings' not found, did you mean:
  command 'strings' from deb binutils
Try: sudo apt install <deb name>
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo apt install binutils
[sudo] password for kali: 
binutils is already the newest version (2.46-3).
binutils set to manually installed.
Summary:                    
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 0
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ srings -n 10 garden.jpg  
Command 'srings' not found, did you mean:
  command 'strings' from deb binutils
Try: sudo apt install <deb name>
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ srings -n 10 garden.jpg 
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ ^[[200~sudo apt install <deb name>
zsh: parse error near `\n'
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo apt install <deb name>  
zsh: parse error near `\n'
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo apt install deb binutil> 
zsh: parse error near `\n'
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo apt install deb binutils
Error: Unable to locate package deb
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ sudo apt install binutils    
binutils is already the newest version (2.46-3).
Summary:                    
  Upgrading: 0, Installing: 0, Removing: 0, Not Upgrading: 0
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ srings -n 10 garden.jpg           
Command 'srings' not found, did you mean:
  command 'strings' from deb binutils
Try: sudo apt install <deb name>
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ 

─$ strings -n 10 garden.jpg 
XICC_PROFILE
mntrRGB XYZ 
Copyright (c) 1998 Hewlett-Packard Company
sRGB IEC61966-2.1
sRGB IEC61966-2.1
IEC http://www.iec.ch
IEC http://www.iec.ch
.IEC 61966-2.1 Default RGB colour space - sRGB
.IEC 61966-2.1 Default RGB colour space - sRGB
,Reference Viewing Condition in IEC61966-2.1
,Reference Viewing Condition in IEC61966-2.1
        %       :       O       d       y
#*%%*525EE\
#*%%*525EE\
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
jVRVik#'        E
Kqk,*[zHW s
.n"Vg`8,2Mz
+^+}N/}7-^
(.Zm')[M_n
kHlmmWlpg/
@:W7ykc<RK4j
h       wvgpZ%!T
oKlqv6QYZy
jO$Q\oe8!G
{We:qN)-Zvf
z;7^}k,6        8:|
.ji[[&cF4qU
fU$P>Rx?J-
 ,J?!^ouyd
|f]8{hJVJ)
}>g<\gn_u5{4x
DVF?t7<}=+
l[Muyqp&#m
zxjRi9Is~F
=GcQZY^Egh
#<m;q^m_iZ
Y|Soif&YFQO=95
.fkBx'"Bx@
VrjN2I'm69
+Fpi>^[[]N
[Gq     ;x9*{WC{
5yo/$YJF0v
m6%bq{*ztM
_;$Mo#FF0F+
l5{mWOh/c*
F5      'r2     ,2=
vIidlkqJn7
yIn+v]N;M:T
'n~_SJm;->
zj0Z\XI8vL
bm.saewewlD
l=:IsB7rmI=w
I/-mr8<%bad
E9-m{_Vg7G
[\}Qn%[wo,
Fn+M7?N|Co
*y}-5VItW=7
cU*T_,uR]QX
<9yd53"\Aj
zx|5:Xx({h
Ksi#E2)a!=
qn;w<%,.nnv
kt}L15!E:p
_c^mHEUUoy]]_F
w{sog3m@8V+
Hn#7.70PS8;
_AQUsKk?=n]
Y=L4%)^I=-
3k$7[@|`tl
*D[X    0rFGj
)n%U`8$7j+
*E4RJC&FG'
su*(~$7z;^
OzWfwrN:VL
5:wZigm=w&
w:m_R7RDT`z
UZzkmu9eQ)=
hIINJ1Q[kgc
}7;=rdk[ub
Z2.]NGpONM:
BkR>i!>iB=
IpWTKFT$)8
M=u4wi'&Cif
=1H"#b0',8
hlk7pi6?iwL
aa,yD=E}..
3`|9pu]F9~C3
6RHK>e\oB:g
v0,'x^D99]
}4s,5'*x,<.
Fquau);^=l|
Pj2Oe2M:DR<
%F7}3_)x        u
*}r=sNFK}.e#
mN5'MBNPm?
09>WE:1NMiRz
ZRikwmum#|5iS
Y#B|+4;AlK ]
o<S#yrG dld
pEtN.mm.mle
\GhZY?y'oA
6L4n>R;r}+
wae:uc(>YwG
Here is a flag: academy{more_than_m33ts_the_3y3ff3b9e86}


```

## NOTAS ADICIONALES
- Saca las cadenas de la imagen ese comando

## REFERENCIAS
https://learn.cylabacademy.org/assignments/12910/44