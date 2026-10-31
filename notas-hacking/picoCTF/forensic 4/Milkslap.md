

## DESCRIPCION
- 🥛 [http://chatelaine.cylabacademy.net:43637/](http://chatelaine.cylabacademy.net:43637/)
## SOLUCION

```
- Se accedió al enlace web proporcionado en la descripción del reto.
    
- Utilizando las herramientas de desarrollador del navegador web, se inspeccionó el tráfico de red (Network) y los elementos estructurales de la página.
    
- Se identificó que la página utilizaba una imagen específica como recurso visual, denominada `concat_v.png`.
    
- Se extrajo y descargó dicha imagen al entorno local (Kali Linux) para realizar un análisis forense.
    
- Sabiendo que la imagen podría contener información oculta, se utilizó la herramienta `zsteg`, la cual está diseñada para detectar datos ocultos en archivos PNG y BMP mediante esteganografía.
    
- _Nota sobre la ejecución:_ Al intentar realizar un escaneo exhaustivo (`zsteg -a`), se presentó un error de desbordamiento de memoria (`stack level too deep (SystemStackError)`) debido a los límites de recursión en las librerías de Ruby. Se procedió a ejecutar el escaneo básico (`zsteg concat_v.png`) o utilizar alternativas web para extraer los datos LSB estándar.
    
- Al procesar la imagen con éxito, la herramienta extrajo los datos del bit menos significativo (LSB) y reveló la bandera en texto claro en la salida de la terminal.
```

## NOTAS ADICIONALES
- Inspección de Assets Web y Esteganografía LSB: Este reto demuestra que, en la categoría forense, las instancias web no siempre implican la explotación de vulnerabilidades de servidor, sino que actúan como un medio para distribuir la evidencia (archivos multimedia). La esteganografía LSB (Least Significant Bit) es una técnica donde se alteran los últimos bits de los valores de color en los píxeles para esconder un mensaje. Esta alteración es visualmente imperceptible, pero herramientas especializadas reconstruyen el mensaje secreto concatenando esos bits alterados.
## REFERENCIAS
-  Reto original: picoCTF 2021 - Categoría: Forensics (Medium).
- Conceptos aplicados: Web Element Inspection, Steganography, LSB Data Extraction, `zsteg`.