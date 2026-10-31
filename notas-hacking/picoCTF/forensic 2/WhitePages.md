
## **DESCRIPCION** 
- I stopped using YellowPages and moved onto WhitePages... but the page they gave me is all blank!

## **SOLUCION**

1. Al descargar el archivo de texto proporcionado, este parece estar completamente vacío al abrirlo en un editor normal.
    
2. Se utiliza el comando `xxd whitepages.txt | head -n 15` en la terminal para inspeccionar el contenido hexadecimal del archivo.
    
3. El análisis revela que el archivo no está vacío, sino compuesto por una secuencia de dos caracteres invisibles: el espacio estándar (`20` en hexadecimal) y un espacio ancho de Unicode (`e280 83` en hexadecimal).
    
4. Se deduce que estos dos espacios representan un código binario (ceros y unos).
    
5. Se crea un script en Python que lee el archivo en modo binario (`rb`), reemplaza el espacio Unicode (`\xe2\x80\x83`) por `0` y el espacio normal (`\x20`) por `1`.
    
6. El script agrupa la cadena binaria resultante en bloques de 8 bits (1 byte) y los convierte a texto usando la función `chr(int(byte, 2))`, lo que revela la bandera oculta.
    

## **NOTAS ADICIONALES**

Este reto pertenece a la categoría de Análisis Forense y utiliza esteganografía basada en texto. Es un método común en competiciones CTF (Capture The Flag) aprovechar caracteres no imprimibles o diferentes variaciones de espacios en la tabla Unicode para ocultar información sin alterar la apariencia visual de un archivo. Siempre es recomendable usar editores o visores hexadecimales al enfrentarse a archivos que parecen estar corruptos o vacíos.

## **REFERENCIAS**

- Reto "WhitePages" creado por John Hammond para picoCTF 2019.
    
- Herramienta `xxd` de Linux para visualización de volcados hexadecimales.
    
- Tabla de caracteres Unicode (Em Space).