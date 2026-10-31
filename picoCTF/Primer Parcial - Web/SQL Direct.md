
## DESCRIPCION

- Connect to this PostgreSQL server and find the flag! `psql -h chatelaine.cylabacademy.net -p 33686 -U postgres pico`

Password is `postgres`

## SOLUCION

```

Se estableció una conexión remota directa con el servidor de bases de datos PostgreSQL utilizando la herramienta de interfaz de línea de comandos `psql`. Se definieron los parámetros de host, puerto, usuario y base de datos mediante el comando proporcionado: `psql -h chatelaine.cylabacademy.net -p 33686 -U postgres pico`.

- Se ingresó la contraseña correspondiente (`postgres`) para autenticar la sesión e ingresar exitosamente al entorno de la base de datos.
    
- Una vez dentro del intérprete interactivo de PostgreSQL (identificado por el prompt `pico=#`), se procedió a enumerar las tablas disponibles. Para ello, se utilizó el meta-comando específico del cliente `\dt`, el cual lista todas las relaciones dentro del esquema actual.
    
- Al identificar la tabla objetivo que almacenaba la información confidencial (por ejemplo, la tabla `flags`), se procedió a extraer su contenido.
    
- Se formuló y ejecutó la consulta SQL estándar `SELECT * FROM flags;` para recuperar todos los registros almacenados en dicha tabla. Los resultados impresos en la consola revelaron directamente la bandera del reto.
```

## NOTAS ADICIONALES

## REFERENCIAS