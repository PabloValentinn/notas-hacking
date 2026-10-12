
## DESCRIPCION
- Decrypt this message. Message: [message](https://challenge-files.cylabacademy.net/library/eb4325fac37933de66857090e6c78c226267394ccaf5c079ff593e3e33b4b95a/data.enc)
## SOLUCION
```
- Se descargó el archivo cifrado `data.enc` utilizando la herramienta `wget` en la terminal.
    
- Se visualizó el contenido del archivo con el comando `cat data.enc`, el cual mostró la cadena `academy{jyvzzpunaolybipjvubsxjvqwk}`.
    
- Se determinó que el texto contenido dentro de las llaves estaba oculto mediante el Cifrado César (un cifrado de sustitución por desplazamiento).
    
- Se aplicó un ataque de fuerza bruta probando los 25 desplazamientos posibles del alfabeto sobre la cadena `jyvzzpunaolybipjvubsxjvqwk`.
    
- Se descubrió que al desplazar los caracteres exactamente 19 posiciones hacia adelante, el texto revelaba la frase en inglés `crossingtherubiconulqcojpd`.
    
- Se ensambló la bandera final respetando estrictamente la envoltura (`academy{ }`) proporcionada por la plataforma personalizada, resultando en `academy{crossingtherubiconulqcojpd}`.

academy{crossingtherubiconulqcojpd}
```

## NOTAS ADICIONALES
- Criptografía Histórica y Fuerza Bruta: El Cifrado César es uno de los métodos criptográficos más antiguos. Su principal debilidad radica en su minúsculo espacio de claves (solo 25 desplazamientos posibles en el abecedario inglés), lo que lo hace completamente vulnerable a ataques de fuerza bruta automatizados o manuales. El mensaje descifrado ("Crossing the Rubicon") hace referencia a un evento histórico real protagonizado por Julio César, sirviendo como un indicador de compromiso (o en este caso, de éxito) que confirma la validez del método de decodificación. Adicionalmente, el reto enfatiza la atención al detalle al requerir que el jugador adapte el formato de envío a los estándares de la plataforma anfitriona (Cylab Academy).

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Cifrado César, Criptografía de Sustitución Clásica, Ataque de Fuerza Bruta.