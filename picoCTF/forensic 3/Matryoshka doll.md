
## DESCRIPCION
- Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [dolls.jpg](https://challenge-files.cylabacademy.net/library/2eb277d09563812ad880fdd564d0fb59c084a64f514f6e12998534c8f7997405/dolls.jpg)

## SOLUCION
```

┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ wget https://challenge-files.cylabacademy.net/library/2eb277d09563812ad880fdd564d0fb59c084a64f514f6e12998534c8f7997405/dolls.jpg   
--2026-10-05 12:52:43--  https://challenge-files.cylabacademy.net/library/2eb277d09563812ad880fdd564d0fb59c084a64f514f6e12998534c8f7997405/dolls.jpg
Resolving challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)... 18.238.132.115, 18.238.132.49, 18.238.132.26, ...
Connecting to challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)|18.238.132.115|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 651609 (636K) [application/octet-stream]
Saving to: ‘dolls.jpg’

dolls.jpg                100%[==================================>] 636.34K  14.1KB/s    in 54s     

2026-10-05 12:53:42 (11.8 KB/s) - ‘dolls.jpg’ saved [651609/651609]

                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ sudo apt install w                                           
Completing package
w1retap                                 wig                                   
w1retap-doc                             wigeon                                
w1retap-mysql                           wiggle                                
w1retap-odbc                            wig-ng                                
w1retap-pgsql                           wiipdf                                
w1retap-sqlite                          wike                                  
w2do                                    wiki2beamer                           
w3cam                                   wikiextractor                         
w3c-linkchecker                         wikipedia2text                        
w3c-markup-validator                    wikitrans                             
w3c-sgml-lib                            wildmidi                              
w3m                                     wiliki                                
w3m-el                                  wily                                  
w3m-el-snapshot                         wims                                  
w3m-img                                 wims-lti                              
waagent                                 wims-modules                          
wabt                                    wimtools                              
wadc                                    winbind                               
waffle-utils                            windowlab                             
wafw00f                                 windows-binaries                      
wah-plugins                             windows-el                            
wait4x                                  window-size                           
wait-for-it                             windows-privesc-check                 
wajig                                   wine                                  
wakeonlan                               wine64                                
walldns                                 wine64-preloader                      
wallstreet                              wine64-tools                          
wamerican                               wine-binfmt                           
wamerican-huge                          wine-common                           
wamerican-insane                        winff                                 
wamerican-large                         winff-data                            
wamerican-small                         winff-doc                             
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ sudo apt install bin
Completing package
bin86                                    binutils-gold-sparc-linux-gnu          
binaryen                                 binutils-gold-sparc-linux-gnu-dbg      
binclock                                 binutils-gold-x86-64-gnu               
bincrypter                               binutils-gold-x86-64-gnu-dbg           
bind9                                    binutils-gold-x86-64-linux-gnu         
bind9-dev                                binutils-gold-x86-64-linux-gnu-dbg     
bind9-dnsutils                           binutils-gold-x86-64-linux-gnux32      
bind9-doc                                binutils-gold-x86-64-linux-gnux32-dbg  
bind9-host                               binutils-h8300-hms                     
bind9-libs                               binutils-hppa64-linux-gnu              
bind9-utils                              binutils-hppa64-linux-gnu-dbg          
bindechexascii                           binutils-hppa-linux-gnu                
bindfs                                   binutils-hppa-linux-gnu-dbg            
bindgen                                  binutils-i686-gnu                      
binfmtc                                  binutils-i686-gnu-dbg                  
binfmt-support                           binutils-i686-linux-gnu                
bing-ip2hosts                            binutils-i686-linux-gnu-dbg            
bingo                                    binutils-loongarch64-linux-gnu         
biniax2                                  binutils-loongarch64-linux-gnu-dbg     
biniax2-data                             binutils-m68hc1x                       
binkd                                    binutils-m68k-linux-gnu                
bino                                     binutils-m68k-linux-gnu-dbg            
binpac                                   binutils-mingw-w64                     
binstats                                 binutils-mingw-w64-all                 
binutils                                 binutils-mingw-w64-base                
binutils-aarch64-linux-gnu               binutils-mingw-w64-i686                
binutils-aarch64-linux-gnu-dbg           binutils-mingw-w64-i686-ucrt           
binutils-aarch64-none-elf                binutils-mingw-w64-ucrt64              
binutils-alpha-linux-gnu                 binutils-mingw-w64-x86-64              
binutils-alpha-linux-gnu-dbg             binutils-mingw-w64-x86-64-ucrt         
binutils-arc-linux-gnu                   binutils-msp430-unknown-elf            
binutils-arc-linux-gnu-dbg               binutils-multiarch                     
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ sudo apt install binwalk
[sudo] password for kali: 
Upgrading:                      
  binwalk  python3-binwalk
                                                                                                    
Summary:
  Upgrading: 2, Installing: 0, Removing: 0, Not Upgrading: 1402
  Download size: 128 kB
  Space needed: 2,048 B / 60.8 GB available

Continue? [Y/n] ^[[A^[[A^C
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ binwalk dolls.jpg       

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378929, uncompressed size: 383919, name: base_images/2_c.jpg
651587        0x9F143         End of Zip archive, footer length: 22

                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ ls -la 
total 648
drwxrwxr-x 2 kali kali   4096 Oct  5 12:52 .
drwxrwxr-x 5 kali kali   4096 Oct  5 12:52 ..
-rw-rw-r-- 1 kali kali 651609 Sep 22 22:37 dolls.jpg
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ unzip dolls.jpg 
Archive:  dolls.jpg
warning [dolls.jpg]:  272492 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/2_c.jpg     
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska]
└─$ cd base_images 
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images]
└─$ ls    
2_c.jpg
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images]
└─$ unzip 2_c.jpg  
Archive:  2_c.jpg
warning [2_c.jpg]:  187707 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/3_c.jpg     
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images]
└─$ cd base_images/ 
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images/base_images]
└─$ ls
3_c.jpg
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images/base_images]
└─$ unzip 2_c.jpg
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images/base_images]
└─$ unzip 3_c.jpg 
Archive:  3_c.jpg
warning [3_c.jpg]:  123606 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/4_c.jpg     
                                                                                                    
┌──(kali㉿kali)-[~/picoctf/matrioska/base_images/base_images]
└─$ cd base_images 
                                                                                                    
┌──(kali㉿kali)-[~/…/matrioska/base_images/base_images/base_images]
└─$ ls
'4_c.jpg
                                                                                                    
┌──(kali㉿kali)-[~/…/matrioska/base_images/base_images/base_images]
└─$ unzip 4_c.jpg 
Archive:  4_c.jpg
warning [4_c.jpg]:  79578 extra bytes at beginning or within zipfile
  (attempting to process anyway)
 extracting: flag.txt                
                                                                                                    
┌──(kali㉿kali)-[~/…/matrioska/base_images/base_images/base_images]
└─$ cat flag.txt    
academy{ZNTyvSDXRNO1d0xCkBRMhAoiafpCTvgW}
                                                                                                    
┌──(kali㉿kali)-[~/…/matrioska/base_images/base_images/base_images]
└─$             

```

## NOTAS ADICIONALES
- Archivos Anidados y Análisis de Firmas (Magic Bytes): Este desafío ilustra un concepto fundamental en el análisis forense digital y la esteganografía. Muchos formatos de archivo (como los archivos ZIP) son identificados por las herramientas del sistema operativo mediante "firmas" o "números mágicos" ubicados en ciertas partes del archivo, no solo por su extensión (como `.jpg`). Cuando se concatena un archivo ZIP al final de una imagen JPEG auténtica, los visores de imágenes estándar mostrarán la foto sin problemas (ya que detienen su lectura en el marcador de fin de imagen), mientras que utilidades como `unzip` o `binwalk` escanearán el archivo, encontrarán las firmas del ZIP oculto y permitirán extraer su contenido sin que la extensión original sea un impedimento.

## REFERENCIAS
- - Reto original: picoCTF 2021 - Categoría: Forensics (Matryoshka doll).
    
- Conceptos aplicados: Steganography, File Concatenation, File Carving, Recursion, Command Line Utilities (`unzip`).
