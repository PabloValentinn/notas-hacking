## DESCRIPCION
 - I made a cool website where you can announce whatever you want! Try it out! I heard templating is a cool and modular way to build web apps! Check out my website [here](http://chatelaine.cylabacademy.net:17219/)!

## SOLUCION

```

- Se accedió a la aplicación web proporcionada por el reto, la cual constaba de un formulario que permitía a los usuarios introducir un anuncio de texto. Se observó que el texto ingresado era posteriormente renderizado en la página de respuesta.
    
- Se realizaron pruebas de inyección básica para identificar el motor de plantillas subyacente. Se introdujo la expresión matemática `{{7*7}}` en el campo de anuncio. La aplicación devolvió el resultado `49`, confirmando una vulnerabilidad de **Server-Side Template Injection (SSTI)** en un entorno Python (probablemente Jinja2/Flask).
    
- Se procedió a la enumeración del sistema. Se inyectó un payload para listar los archivos del directorio de trabajo actual, utilizando el acceso a objetos internos de Python: `{{ ''.__class__.__mro__[1].__subclasses__() }}` o mediante el uso de `os.popen`. El listado reveló la presencia de archivos críticos: `__pycache__`, `app.py`, `requirements.txt` y un archivo llamado `flag`.
    
- Se construyó un payload específico para leer el contenido del archivo `flag`. Dado que el entorno permite el acceso a módulos del sistema, se utilizó el objeto global `cycler` de Jinja2 para alcanzar el módulo `os` y ejecutar comandos del sistema operativo.
    
- Se ejecutó el payload final: `{{ cycler.__init__.__globals__.os.popen('cat flag').read() }}`. El motor de plantillas evaluó la expresión, ejecutó el comando `cat flag` en el servidor y devolvió el contenido del archivo en la respuesta HTTP.
    
- La bandera obtenida fue: `picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_9451989d}`.
```

## NOTAS ADICIONALES
- - **Server-Side Template Injection (SSTI):** Esta vulnerabilidad ocurre cuando una aplicación web incrusta la entrada del usuario directamente en una plantilla del lado del servidor sin la sanitización adecuada. A diferencia de XSS (que ocurre en el cliente), SSTI permite al atacante ejecutar código en el servidor. En Python (Jinja2), esto puede llevar a la ejecución remota de comandos (RCE) mediante el acceso a objetos internos de Python (`__class__`, `__mro__`, `__subclasses__`, `__globals__`, `__builtins__`).
    
- **Uso de `cycler` para RCE:** El objeto `cycler` es una función global disponible en el contexto de Jinja2. A través de `cycler.__init__.__globals__`, se puede acceder al diccionario de variables globales del módulo `jinja2.utils`, donde reside el módulo `os`. Esto permite ejecutar comandos del sistema operativo (como `cat flag`) directamente desde la plantilla, evadiendo posibles restricciones de sandbox si no están correctamente configuradas.
    
- **Impacto:** La explotación exitosa de SSTI permite a un atacante leer archivos sensibles (como el código fuente `app.py` o la `flag`), ejecutar comandos arbitrarios en el sistema operativo, y potencialmente comprometer completamente el servidor.
    
- **Prevención:** Para prevenir SSTI, se debe evitar el renderizado dinámico de plantillas con entrada del usuario. Si es inevitable, se deben utilizar funciones de escape y sanitización estrictas, o utilizar motores de plantillas "sandbox" que limiten el acceso a objetos peligrosos de Python.

## REFERENCIAS
- - Reto original: picoCTF 2025 - Categoría: Web Exploitation (SSTI1).
    
- Conceptos aplicados: Server-Side Template Injection (SSTI), Jinja2, Python Sandbox Escape, Remote Code Execution (RCE), File Inclusion.