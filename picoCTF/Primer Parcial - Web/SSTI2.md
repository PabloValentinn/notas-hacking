

## DESCRIPCION

- I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :) I heard templating is a cool and modular way to build web apps! Check out my website [here](http://chatelaine.cylabacademy.net:34813/)!
## SOLUCION

```

- Se accedió a la aplicación web proporcionada por el reto, la cual presentaba una funcionalidad similar al reto anterior (SSTI1) pero con un filtro de seguridad implementado. El enunciado indicaba que se eliminaban caracteres problemáticos para prevenir inyecciones.
    
- Se realizaron pruebas de inyección básica con el payload `{{7*7}}`. La aplicación devolvió `49`, confirmando que la vulnerabilidad de **Server-Side Template Injection (SSTI)** persistía en el entorno Python (Jinja2/Flask).
    
- Se intentó explotar la vulnerabilidad utilizando el payload estándar de SSTI1: `{{ cycler.__init__.__globals__.os.popen('cat flag').read() }}`. La aplicación respondió con el mensaje de error personalizado: `Stop trying to break me >:(`, confirmando la presencia de un filtro de lista negra (Blacklist Filter) que bloqueaba caracteres como guiones bajos (`_`), puntos (`.`), corchetes (`[`, `]`), y palabras clave como `os`, `popen`, `class`, `globals`, etc.
    
- Se procedió a evadir el filtro mediante técnicas de ofuscación. Se utilizó la codificación hexadecimal para representar los guiones bajos (`_` -> `\x5f`) y se reemplazó el acceso a atributos mediante puntos (`.`) por el filtro `|attr()` de Jinja2. Asimismo, se sustituyó el acceso a índices mediante corchetes (`[]`) por el método `__getitem__`, también ofuscado.
    
- Se construyó el payload final ofuscado:  
    `{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}`
    
- Se introdujo este payload en el campo de anuncio de la página principal (evitando la ruta `/announce` que devolvía un mensaje de redirección). El servidor procesó la plantilla, ejecutó el comando `cat flag` a través del módulo `os` importado dinámicamente, y devolvió el contenido del archivo en la respuesta HTTP.
    
- La bandera obtenida fue: `picoCTF{sst1_f1lt3r_byp4ss_...}`.
```

## NOTAS ADICIONALES

- - **Bypass de Filtros mediante Ofuscación:** Los filtros de lista negra (Blacklist) que bloquean caracteres o palabras clave específicas son inherentemente débiles. Los atacantes pueden evadirlos utilizando representaciones alternativas de los mismos caracteres (como codificación hexadecimal, octal o Unicode) o utilizando funcionalidades nativas del motor de plantillas (como el filtro `attr()` en Jinja2) que permiten el acceso a atributos sin usar la sintaxis convencional bloqueada.
    
- **Uso de `|attr()` y `__getitem__`:** El filtro `attr()` permite acceder a atributos de un objeto sin usar el punto (`.`). El método `__getitem__` permite acceder a elementos de un diccionario o lista sin usar corchetes (`[]`). Al codificar los guiones bajos como `\x5f`, se evita que el filtro reconozca las palabras clave como `__globals__` o `__builtins__`, permitiendo la ejecución remota de comandos (RCE) y la lectura de archivos sensibles.
    
- **Impacto:** La explotación exitosa de SSTI con evasión de filtros permite a un atacante eludir las medidas de seguridad implementadas por el desarrollador, ejecutar comandos arbitrarios en el servidor y comprometer completamente el sistema, accediendo a archivos confidenciales como la bandera del reto.
    
- **Prevención:** Para prevenir SSTI de forma efectiva, no basta con implementar listas negras de caracteres. Se debe evitar el renderizado dinámico de plantillas con entrada del usuario. Si es inevitable, se deben utilizar motores de plantillas "sandbox" que limiten el acceso a objetos peligrosos de Python, o implementar listas blancas (Whitelist) estrictas que solo permitan caracteres seguros.


## REFERENCIAS
- - Reto original: picoCTF 2025 - Categoría: Web Exploitation (SSTI2).
    
- Conceptos aplicados: Server-Side Template Injection (SSTI), Jinja2, Blacklist Bypass, Hexadecimal Encoding, Python Sandbox Escape, Remote Code Execution (RCE), File Inclusion.