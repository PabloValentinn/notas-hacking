
## DESCRIPCION
- Decode this [message](https://challenge-files.cylabacademy.net/library/d825fde6581b1311eafdd403da1cc96f1f98fe3fe84cd71d850310ebb3908088/message.wav) from the moon.

## SOLUCION
```

Primero descargue el archivo de audio que me venia en el link. Luego le di pip install sstv pero me dio error. Despues puse los siguientes comandos: 

$ python -m venv mivenv
                                                                             
┌──(kali㉿kali)-[~/cylab]
└─$ source mivenv/bin/activate                                   
                                                                             
┌──(mivenv)─(kali㉿kali)-[~/cylab]
└─$ sstv -d message.wav -o flag.png

donde te daba una imagen con la bandera

```

## NOTAS ADICIONALES

## REFERENCIAS
Gemini IA
