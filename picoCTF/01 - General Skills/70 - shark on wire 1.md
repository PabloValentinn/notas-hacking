
## DESCRIPCION
- We found this [packet capture](https://challenge-files.cylabacademy.net/library/e64f2c2aaf9bf531af7be1787c1407c47a4cc7b57f251d5108a1151e9721a2d6/shark-on-wire-1-capture.pcap). Recover the flag.

## SOLUCION
```
wget https://challenge-files.cylabacademy.net/library/e64f2c2aaf9bf531af7be1787c1407c47a4cc7b57f251d5108a1151e9721a2d6/shark-on-wire-1-capture.pcap

(pabloval)-[~]
└─$ sudo apt install wireshark

abrimos wireshark
abrimos el archivo y buscamos uno que sea UDP, para poder buscar la flag correspondiente

```
## NOTAS ADICIONALES

## REFERENCIAS
wireshark