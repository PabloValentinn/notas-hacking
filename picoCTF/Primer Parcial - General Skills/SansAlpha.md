

## DESCRIPCION

- The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols. `ssh -p 13293 ctf-player@chatelaine.cylabacademy.net`

Use password: `fa1a82ad`

## SOLUCION

```

Aquí tienes la documentación final para este desafío, redactada con el formato formal detallando toda la progresión técnica que realizamos para evadir el filtro:

**SansAlpha**

DESCRIPCION The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.

SOLUCION

- Se estableció una conexión SSH con la instancia del reto, accediendo a un entorno de shell altamente restrictivo ("SansAlpha") que bloqueaba e ignoraba cualquier pulsación de teclas alfabéticas.
    
- Se probaron técnicas iniciales de _ANSI-C Quoting_ (caracteres octales) e intentos de escape del intérprete de comandos mediante variables especiales (`$0`), las cuales fueron neutralizadas por el filtro del servidor.
    
- Se implementó una técnica de evasión basada en la expansión de comodines (wildcards) del sistema de archivos. Se utilizó el patrón `/???/????64 *` para invocar ciegamente el binario `/bin/base64` sobre los archivos del directorio actual.
    
- Al forzar la ejecución, el análisis de los errores estándar de la consola (`extra operand 'blargh'` y `extra operand 'on-calastran.txt'`) permitió realizar un mapeo a ciegas del directorio, revelando la existencia de la carpeta `blargh` y de archivos de texto distractorios.
    
- Se detectó una colisión en los comodines, ya que `????64` coincidía tanto con `base64` como con `x86_64`. Se ajustó la expresión regular utilizando una negación de rango numérico `[!0-9]` para aislar exclusivamente al programa `base64`.
    
- Sabiendo que la bandera se encontraba dentro del directorio de seis letras (`blargh`), se construyó un patrón de comodines con la longitud exacta del archivo objetivo (`flag.txt` -> `????.???`) para evitar el error de múltiples operandos.
    
- Se ejecutó el _bypass_ final en el servidor con el comando: `/???/?[!0-9]??64 ??????/????.???`
    
- El intérprete expandió correctamente el patrón a `/bin/base64 blargh/flag.txt`, devolviendo el contenido cifrado del archivo en la salida estándar.
    
- Se copió el bloque de texto devuelto, se trasladó a una terminal local sin restricciones y se decodificó exitosamente ejecutando `echo "[TEXTO]" | base64 -d`, lo que imprimió la bandera definitiva.
```

## NOTAS ADICIONALES

- Bypass de Filtros y Expansión de Comodines (Wildcard Globbing): En los sistemas basados en UNIX, el intérprete de comandos (Shell) evalúa y expande los comodines antes de pasar los argumentos resultantes a los binarios. El comodín `?` sustituye exactamente a un carácter cualquiera, mientras que las clases de caracteres como `[!0-9]` excluyen patrones específicos (en este caso, cualquier dígito). Este reto demuestra cómo un atacante o auditor de seguridad puede abusar de la evaluación nativa del shell para ejecutar comandos del sistema, navegar por rutas y leer archivos confidenciales basándose únicamente en la longitud y metadatos de los nombres, vulnerando exitosamente filtros de entrada (Input Validation) que prohíben el uso del teclado alfabético.

## REFERENCIAS

- - Reto original: picoCTF 2024 - Categoría: General Skills (SansAlpha).
    
- Conceptos aplicados: Shell Escaping, Wildcard Expansion, Base64 Encoding/Decoding, Bypassing Alphanumeric Filters.