
## DESCRIPCION

- The Rust saga continues? I ask you, can I borrow that, pleeeeeaaaasseeeee?

Download the Rust code [here](https://challenge-files.cylabacademy.net/library/048c73621a97b98cde18eae5a9495279f2396cb64c65235bb310e7ad26d726ac/fixme2.tar.gz).

## SOLUCION

```

- Se descargó el código fuente empaquetado del reto (`fixme2.tar.gz`) en el entorno local de Linux, debido a que el desafío especificaba que no era compatible con la webshell de la plataforma.
    
- Se extrajo el contenido del archivo comprimido utilizando el comando `tar -xzf` y se accedió al nuevo directorio del proyecto, el cual mantenía la estructura estándar administrada por Cargo.
    
- Se intentó construir y ejecutar el programa inicialmente con el comando `cargo run`. El compilador detuvo la ejecución y arrojó el error `E0596`, advirtiendo que no se podía tomar prestada la variable como mutable porque estaba detrás de una referencia inmutable.
    
- Se analizó el archivo `src/main.rs` (específicamente la línea 3) y se identificó que la función `decrypt` intentaba modificar la cadena `borrowed_string`, pero el parámetro estaba definido como una referencia de solo lectura. Se corrigió la firma de la función agregando el identificador de mutabilidad: `&mut String`.
    
- Al intentar compilar de nuevo, el sistema detuvo el proceso con un segundo error, esta vez por tipos incompatibles (`E0308: mismatched types`). El compilador detectó una incongruencia entre lo que pedía la función (una referencia mutable) y lo que se le estaba enviando en su invocación.
    
- Se editó nuevamente el archivo en la línea 35 para ajustar la llamada a la función, cambiando el argumento original `&party_foul` por un pase de referencia explícitamente mutable: `&mut party_foul`.
    
- Tras guardar los cambios, se ejecutó `cargo run` por última vez. El compilador validó correctamente los permisos de memoria, ejecutó el programa sin contratiempos y este imprimió exitosamente la bandera en la terminal.
```

## NOTAS ADICIONALES

- El Borrow Checker y la Mutabilidad Explícita: Rust se distingue por garantizar la seguridad de memoria en tiempo de compilación mediante su sistema de propiedad (Ownership) y préstamo (Borrowing). Por diseño, todas las variables y referencias son inmutables por defecto. Si una función requiere modificar una variable sin ser la "dueña" de la misma, debe solicitar un préstamo mutable (`&mut`). Este reto demuestra una de las reglas más estrictas de Rust: la mutabilidad debe ser completamente explícita y bidireccional; el programador debe declarar la intención de modificar la variable tanto en la definición de la función que la recibe, como en la línea exacta donde la variable es enviada.

## REFERENCIAS
- - Reto original: picoCTF 2025 - Categoría: General Skills (Rust fixme 2).
    
- Documentación de herramientas: "The Rust Programming Language" (El Libro de Rust) - Capítulo 4: Understanding Ownership (Sección: References and Borrowing).