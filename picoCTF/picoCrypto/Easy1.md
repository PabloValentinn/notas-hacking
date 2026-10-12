

## DESCRIPCION
- The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help UFJKXQZQUNB with the key of SOLVECRYPTO. Can you use this table to solve it?

## SOLUCION
```
- Se analizó la descripción del desafío, la cual entregaba tres elementos clave: el texto cifrado (`UFJKXQZQUNB`), la llave criptográfica (`SOLVECRYPTO`) y un enlace a una tabla de ayuda.
    
- Se identificó que la tabla proporcionada correspondía al Cuadro de Vigenère, indicando que el método criptográfico utilizado era un cifrado polialfabético clásico, y no un verdadero _One Time Pad_ (Libreta de un solo uso).
    
- Se decodificó el mensaje manualmente relacionando cada letra del texto cifrado con su correspondiente letra en la llave a través de las intersecciones de la tabla de Vigenère.
    
- El proceso de sustitución inversa reveló el texto en claro `CRYPTOISFUN`, el cual se combinó con el formato de envoltura requerido para obtener la bandera final `picoCTF{CRYPTOISFUN}` (o `academy{CRYPTOISFUN}`).
  
  academy{CRYPTOISFUN}
```

## NOTAS ADICIONALES
- Cifrado Vigenère vs. One Time Pad (OTP): Este reto ilustra una distinción fundamental en criptografía. Un verdadero _One Time Pad_ es matemáticamente irrompible (secreto perfecto) porque requiere una llave completamente aleatoria, de la misma longitud que el mensaje, y que jamás se reutilice. Por el contrario, este desafío utiliza el Cifrado de Vigenère repitiendo una palabra clave estática y reconocible (`SOLVECRYPTO`). Esta repetición cíclica de la llave crea patrones que hacen al cifrado vulnerable al análisis de frecuencias (como el método Kasiski) en textos más largos, demostrando por qué no posee la seguridad absoluta de un OTP.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Cifrado de Vigenère, Criptografía Polialfabética, Teoría de One Time Pad.

