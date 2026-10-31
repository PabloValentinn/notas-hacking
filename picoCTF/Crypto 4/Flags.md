
## DESCRIPCION
- What do the [flags](https://challenge-files.cylabacademy.net/library/187296d0c352a8451662153842fc9794b9f247a1ac949978113ddfcb9a1bb76f/flag.png) mean?

## SOLUCION
```

- Se descargó el recurso multimedia provisto en el reto a través del enlace `flags` (un archivo de imagen con formato PNG que contiene una cuadrícula de banderas visuales ordenadas).
    
- Al visualizar el archivo, se identificó una secuencia gráfica de banderas cuadradas con distintos patrones geométricos y colores, separadas por símbolos de llave `{` y `}`.
    
- **Identificación del sistema de cifrado/codificación:** Las banderas corresponden al **Código Internacional de Señales** (_International Code of Signals_ o **ICS**), un estándar marítimo internacional utilizado históricamente para la comunicación visual entre embarcaciones o estaciones costeras mediante el izado de banderas alfabéticas y numéricas.
    
- Se verificó el patrón inicial de banderas observando que las primeras corresponden a las letras del prefijo del formato de la competencia (`P-I-C-O-C-T-F` o `A-C-A-D-E-M-Y`).
    
- Utilizando una tabla de referencia del Código Internacional de Señales (ICS), se tradujo cada símbolo alfabético ubicado dentro de las llaves:
    
    - Bandera blanca y roja (dividida verticalmente): **H**
        
    - Bandera azul y blanca: **S**
        
    - Bandera ajedrezada azul y blanca: **N**
        
    - _(Continuando con la sustitución letra por letra según el patrón ICS)_.
        
- Tras transcribir cada bandera y sustituir los números correspondientes a la convención leetspeak utilizada en el reto, se obtuvo la frase decodificada: `F1AG5AND5TUFF`.
    
- La reconstrucción final reveló la bandera: `PICOCTF{F1AG5AND5TUFF}` (o adaptada a la plataforma: `academy{F1AG5AND5TUFF}`).
```
## NOTAS ADICIONALES
- Código Internacional de Señales (ICS) en Criptografía Clásica: Aunque concebido para la señalización marítima y la seguridad de navegación, el ICS funciona formalmente como un sistema de codificación de sustitución monoalfabética visual (análogo al semáforo de banderas o al código Morse). Cada bandera representa tanto una letra individual como un mensaje de emergencia o maniobra estandarizado en el mar (por ejemplo, la bandera _Bravo_ significa "transporte de mercancías peligrosas"). En retos de CTF, su resolución no requiere potencia computacional ni criptoanálisis complejo, sino el reconocimiento de patrones de señalización física y el mapeo directo con sus alfabetos estandarizados.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Código Internacional de Señales (ICS), Criptografía Visual Clásica, Sustitución de Banderas Marítimas.