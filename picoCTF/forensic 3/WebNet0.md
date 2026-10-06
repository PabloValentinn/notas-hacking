

## DESCRIPCION

- We found this [packet capture](https://challenge-files.cylabacademy.net/library/2d15538465c5948f0f0626d0cdd271f74363c00aa99d694730fe98331946ab88/webnet0-capture.pcap) and [key](https://challenge-files.cylabacademy.net/library/2d15538465c5948f0f0626d0cdd271f74363c00aa99d694730fe98331946ab88/picopico.key). Recover the flag.

## SOLUCION
```
- Se descargaron los dos archivos proporcionados por el reto: un archivo de captura de red (`packet capture`) y un archivo de llave criptográfica (`key`).
    
- Se abrió el archivo de captura de paquetes (generalmente en formato `.pcap` o `.pcapng`) utilizando la herramienta de análisis de protocolos de red, Wireshark.
    
- Al realizar una inspección inicial del tráfico, se observó que la comunicación entre el cliente y el servidor web estaba cifrada utilizando el protocolo TLS (Transport Layer Security), lo que impedía visualizar el contenido de las peticiones HTTP en texto claro.
    
- Para vulnerar este cifrado, se aprovechó la llave privada (`key`) proporcionada. Se configuró Wireshark para utilizar esta llave e interceptar la comunicación. Esto se logra yendo a la ruta de configuración: `Edit` -> `Preferences` -> `Protocols` -> `TLS` (o `SSL` en versiones antiguas) y añadiendo el archivo de la llave privada en la sección de "RSA keys list".
    
- Una vez cargada la llave privada, Wireshark fue capaz de descifrar retroactivamente los paquetes TLS, revelando todo el tráfico HTTP subyacente.
    
- Se filtró el tráfico en Wireshark utilizando el filtro `http` para aislar las comunicaciones web.
    
- Al inspeccionar los paquetes HTTP ya descifrados (usualmente haciendo clic derecho en un paquete HTTP y seleccionando `Follow` -> `HTTP Stream`, o utilizando la herramienta de búsqueda para la cadena `picoCTF{`), se encontró la bandera. Esta se encontraba oculta dentro de un encabezado (header) HTTP personalizado (típicamente `Pico-Flag:`) en la respuesta del servidor.

Pico-Flag: academy{nongshim.shrimp.crackers}

```
## NOTAS ADICIONALES
- **Descifrado de tráfico TLS pasivo:** Este reto demuestra cómo el tráfico de red protegido por versiones antiguas de TLS (o configuraciones que utilizan intercambio de claves RSA puro en lugar de Perfect Forward Secrecy como (EC)DHE) puede ser descifrado por completo si un atacante o auditor logra comprometer la llave privada RSA del servidor. Al cargar la llave privada en analizadores como Wireshark, el software puede extraer el _Pre-Master Secret_ del tráfico interceptado, derivar las llaves de sesión simétricas y descifrar la captura de paquetes (PCAP) de forma pasiva, exponiendo contraseñas, tokens y, en este caso, la bandera.

## REFERENCIAS
- - Reto original: picoCTF 2019 - Categoría: Forensics (WebNet0).
    
- Conceptos aplicados: Network Traffic Analysis (NTA), Packet Sniffing, TLS/SSL Decryption, HTTP Protocol Analysis, Wireshark.