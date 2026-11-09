
## DESCRIPCION
- The numbers... what do they mean? [numbers](https://challenge-files.cylabacademy.net/library/664bc3a85525cfd5a2af151d29f2744ba334880e28e60f9a513aba13633199d4/the_numbers.png)

## SOLUCION
```
- Se descargó la imagen proporcionada en el reto, la cual mostraba una secuencia numérica estructurada visualmente con el formato de una bandera: `16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }`.
    
- Se analizó el patrón numérico y se identificó el uso de un cifrado de sustitución simple conocido como A1Z26, donde cada número equivale a la posición de una letra en el abecedario inglés (A=1, B=2, C=3... Z=26).
    
- Se realizó la traducción manual mapeando cada bloque numérico a su letra correspondiente. La secuencia inicial `16 9 3 15 3 20 6` se decodificó como `PICOCTF`.
    
- Se continuó con la sustitución de los números ubicados dentro de las llaves, revelando el mensaje en texto claro y componiendo la bandera final: `PICOCTF{THENUMBERSMASON}`.

PICOCTF{THENUMBERSMASON}
```
## NOTAS ADICIONALES
- Criptografía de Sustitución Básica: Este desafío introduce los conceptos fundamentales de la criptografía clásica. El método A1Z26 es un cifrado de sustitución directa que mapea símbolos (enteros decimales) a otros caracteres (alfabéticos) utilizando un índice estático. Aunque carece de una clave secreta y es trivial de descifrar, ilustra la lógica base sobre la cual se construyen métodos de ofuscación y algoritmos históricos más robustos.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Easy).
    
- Conceptos aplicados: Cifrado A1Z26, Criptografía de Sustitución Simple, Decodificación Manual.