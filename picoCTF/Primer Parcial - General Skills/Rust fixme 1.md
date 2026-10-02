
## DESCRIPCION

- Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!

## SOLUCION

```

- Se descargó el código fuente empaquetado del reto (`fixme1.tar.gz`) utilizando la herramienta `wget` dentro del entorno de línea de comandos en Linux.
    
- Se extrajo el contenido del archivo comprimido mediante el comando `tar -xzf fixme1.tar.gz`, revelando la estructura estándar de un proyecto de Rust administrado por Cargo (incluyendo el archivo de configuración `Cargo.toml` y el directorio `src`).
    
- Se intentó construir y ejecutar el proyecto inicial mediante el comando `cargo run`, lo cual resultó en la interrupción del proceso, ya que el estricto compilador de Rust detectó múltiples errores de sintaxis y manejo de memoria en el archivo `src/main.rs`.
    
- Se analizó la detallada salida del compilador y se procedió a editar el código fuente para corregir las siguientes fallas estructurales:
    
    - Se añadió un punto y coma (`;`) faltante al final de la declaración de la variable `key` (línea 5).
        
    - Se insertaron las llaves de formato (`{}`) requeridas dentro de la macro `println!` para permitir la correcta impresión de datos por consola (línea 25).
        
    - Se solucionó un error crítico de propiedad de memoria (_use of moved value_) en el control de flujo. Se reemplazó la mención aislada de la variable `res;` por una instrucción explícita de retorno (`return;`), asegurando que, en caso de error, la función terminara correctamente sin consumir la variable prematuramente.
        
- Tras guardar las correcciones, se volvió a ejecutar el comando `cargo run`. El gestor de paquetes resolvió y descargó las dependencias externas (como el _crate_ `xor_cryptor`), compiló el código fuente de forma exitosa y el programa descifró e imprimió la bandera en la terminal.
```

## NOTAS ADICIONALES

- El Compilador de Rust y Cargo: El lenguaje Rust es ampliamente reconocido en la industria por su compilador (`rustc`). A diferencia de lenguajes como C o C++, el compilador de Rust no solo detiene la ejecución ante fallas (especialmente las relacionadas con la gestión de memoria de su _Borrow Checker_), sino que diagnostica el error de forma proactiva, indicando la línea exacta y sugiriendo fragmentos de código para la reparación. Además, la resolución de este reto demostró la necesidad de usar `cargo` (el gestor de paquetes de Rust) en lugar de compilar el archivo individualmente, ya que el proyecto dependía de librerías criptográficas externas para funcionar.

## REFERENCIAS
- - Reto original: picoCTF 2025 - Categoría: General Skills (Rust fixme 1).
    
- Documentación de herramientas: "The Rust Programming Language" (El Libro de Rust) - Capítulos sobre sintaxis básica, variables y el gestor de paquetes Cargo.