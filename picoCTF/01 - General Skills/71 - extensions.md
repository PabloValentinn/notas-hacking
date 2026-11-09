
## DESCRIPCION
- This is a really weird text file. Can you find the flag? Get the flag from [TXT](https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt).
## SOLUCION
```
┌──(kali㉿kali)-[~]
└─$ wget https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt                    
--2026-09-28 13:16:54--  https://challenge-files.cylabacademy.net/library/a5d365fedad883763fb28c78e25a1765220bef6501848c84f2a7a7adf74d83cd/flag.txt
Resolving challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)... 13.226.187.66, 13.226.187.37, 13.226.187.40, ...
Connecting to challenge-files.cylabacademy.net (challenge-files.cylabacademy.net)|13.226.187.66|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 15696 (15K) [application/octet-stream]
Saving to: ‘flag.txt’

flag.txt                                                   100%[========================================================================================================================================>]  15.33K  --.-KB/s    in 0s      

2026-09-28 13:16:55 (96.9 MB/s) - ‘flag.txt’ saved [15696/15696]

                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ mv flag.txt flags.png
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ open flags.png 
                     
                     
academy{now_you_know_about_extensions}
```

## NOTAS ADICIONALES
- Solo le cambie la extension con mv

## REFERENCIAS
https://learn.cylabacademy.org/assignments/12910/52