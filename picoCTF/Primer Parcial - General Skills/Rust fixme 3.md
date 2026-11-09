
## DESCRIPCION
- Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!

## SOLUCION

```

- Se descargó y extrajo el archivo comprimido correspondiente a la tercera parte del reto (`fixme3.tar.gz`) en un entorno local basado en Linux, acatando la restricción de la plataforma sobre el uso de la webshell.
    
- Se ingresó al directorio raíz del proyecto y se ejecutó el comando `cargo run` para inicializar el proceso de construcción e identificar la falla.
    
- El compilador detuvo la ejecución arrojando un error de nivel de seguridad (`E0133`), advirtiendo que se estaba realizando una llamada a una función insegura (`call to unsafe function`) sin la encapsulación requerida.
    
- Se examinó el archivo de código fuente `src/main.rs` en la línea 31, localizando la función `std::slice::from_raw_parts`. Se identificó que esta función interactúa directamente con punteros crudos en la memoria (`decrypted_ptr`), una acción estrictamente protegida por el compilador de Rust.
    
- Se editó el código para envolver explícitamente dicha llamada dentro de un bloque de código inseguro. La línea original fue modificada para delegar la responsabilidad de seguridad al programador: `let decrypted_slice = unsafe { std::slice::from_raw_parts(decrypted_ptr, decrypted_len) };`.
    
- Tras guardar las modificaciones, se ejecutó nuevamente el proyecto mediante `cargo run`. El compilador validó la sintaxis del bloque inseguro, completó la construcción del binario y el programa se ejecutó satisfactoriamente, descifrando y mostrando la bandera en la salida estándar de la consola.
```
## NOTAS ADICIONALES
 - Bloques Inseguros (Unsafe Rust): Una de las características fundamentales de Rust es su garantía de seguridad de memoria (Memory Safety) en tiempo de compilación, la cual previene vulnerabilidades críticas y comportamientos indefinidos (Undefined Behavior). Sin embargo, cuando la manipulación directa de hardware, la interacción con sistemas operativos o la integración con lenguajes como C o C++ es indispensable, Rust provee la palabra clave `unsafe`. Al utilizar un bloque `unsafe {}`, el desarrollador no desactiva el compilador por completo, pero le indica explícitamente que asumirá la responsabilidad manual de garantizar que las operaciones con punteros crudos no corromperán la memoria.

## REFERENCIAS

- - Reto original: picoCTF 2025 - Categoría: General Skills (Rust fixme 3).
    
- Documentación de herramientas: "The Rust Programming Language" (El Libro de Rust) - Capítulo 19: Advanced Features (Sección: Unsafe Rust).