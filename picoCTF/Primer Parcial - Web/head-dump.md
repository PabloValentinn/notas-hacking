
## DESCRIPCION
- Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.

The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.

## SOLUCION
```

Ingrese al link y me fui al apartado donde decia API documentation. Una vez ahi me salio a que carpeta debia irme. La puse en el navegador y me descargo un archivo que al ponerlo en mi terminal de linux busque la bandera con este comando.

strings heapdump-1790739675554.heapsnapshot | grep "academy{"


academy{Pat!3nt_15_Th3_K3y_9b928e80}

```

## NOTAS ADICIONALES

## REFERENCIAS
Gemini IA