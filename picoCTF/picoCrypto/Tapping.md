

## DESCRIPCION
- Theres tapping coming in from the wires.

## SOLUCION
```
- Se analizó la descripción y el título del reto ("Tapping"), identificando la referencia a "golpeteos en los cables", lo cual es un indicio clásico del uso de Código Morse.
    
- Se estableció la conexión con el servidor remoto utilizando el comando proporcionado en la terminal de Kali Linux: `nc chatelaine.cylabacademy.net 34072`.
    
- El servidor devolvió inmediatamente una cadena de texto compuesta exclusivamente por puntos y guiones: `.- -.-. .- -.. . -- -.-- { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ---.. ---.. -.-. -.-. ----- ----- ..-. ..... }`.
    
- Se procedió a decodificar la cadena utilizando una tabla de traducción de Código Morse (o una herramienta de decodificación online), mapeando cada bloque a su correspondiente carácter alfanumérico.
    
- El proceso de decodificación reveló el texto en claro, arrojando la bandera final del reto: `ACADEMY{M0RS3C0D31SFUN88CC00F5}`.


ACADEMY{M0RS3C0D31SFUN88CC00F5}
```

## NOTAS ADICIONALES
- Codificación Histórica y Telecomunicaciones: El Código Morse, desarrollado en la década de 1830, es un método de codificación de caracteres utilizado primariamente en las telecomunicaciones tempranas (telégrafo). Representa letras y números mediante secuencias estandarizadas de señales de duración corta (puntos) y larga (rayas). Aunque técnicamente no es un sistema de encriptación diseñado para mantener un secreto, sino un esquema de codificación para la transmisión física de datos, es un elemento recurrente en ejercicios de ciberseguridad para enseñar sobre reconocimiento de patrones y conversión de formatos de información.

## REFERENCIAS

- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Código Morse, Telecomunicaciones, Extracción de datos vía Netcat (`nc`).
