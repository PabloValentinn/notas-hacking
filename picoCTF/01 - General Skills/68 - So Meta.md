

## DESCRIPCION
- Find the flag in this [picture](https://challenge-files.cylabacademy.net/library/7ed1ce00a2228a823941d5586923914d39f3085ee0a9a432555322b8dfa9f92e/pico_img.png).

Hints

1 What does meta mean in the context of files?

2 Ever heard of metadata?
## SOLUCION

```


┌──(kali㉿kali)-[~]
└─$ open pico_img.png 
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ exiftool pico_img.png 
ExifTool Version Number         : 13.55
File Name                       : pico_img.png
Directory                       : .
File Size                       : 109 kB
File Modification Date/Time     : 2026:09:22 21:49:10-04:00
File Access Date/Time           : 2026:09:28 12:45:24-04:00
File Inode Change Date/Time     : 2026:09:28 12:44:47-04:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Artist                          : academy{s0_m3ta_b52e28f5}
Image Size                      : 600x600
Megapixels                      : 0.360
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ exiftool -Artist pico_img.png
Artist                          : 


academy{s0_m3ta_b52e28f5}

```

## NOTAS ADICIONALES

- **`exiftool`**: Es una herramienta especializada en leer, escribir y analizar los metadatos (los datos sobre los datos) de archivos multimedia y documentos.
- Es un filtro. En lugar de arrojarte toda la lista de metadatos de la imagen (como la resolución, fecha de creación o modelo de la cámara), le indica al programa que **solo** te interesa ver lo que está escrito en el campo "Artista".
## REFERENCIAS
https://learn.cylabacademy.org/assignments/12910/19