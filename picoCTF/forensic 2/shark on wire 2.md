
## DESCRIPCION
- We found this packet capture. Recover the flag that was pilfered from the network.

## SOLUCION
```

- Se descargó el archivo de captura de tráfico de red (`shark-on-wire-2-capture.pcap`) y se abrió en **Wireshark** para su análisis.
    
- Al inspeccionar los flujos UDP, se aplicó el filtro `udp.port == 22` para aislar tráfico inusual, ya que el puerto 22 suele estar reservado para SSH (TCP) y no para UDP.
    
- Se observó un patrón anómalo en los paquetes enviados desde la IP local (`10.0.0.66`) hacia la IP de destino (`10.0.0.1`): los **puertos de origen (Source Ports)** seguían una secuencia en el rango de los 5000 (ej. 5000, 5097, 5099, 5097, 5100).
    
- Se identificó el método de exfiltración (esteganografía en red): el atacante ocultó los caracteres de la bandera en los números de los puertos de origen. Al restarle 5000 al número del puerto, el resultado equivale al valor decimal ASCII de un carácter (ej. 5097 - 5000 = 97, que corresponde a la letra **'a'**).
    
- Para evitar el cálculo manual paquete por paquete, se automatizó la extracción utilizando herramientas de línea de comandos en Kali Linux (`tshark` para leer la captura y `awk` para la operación matemática y conversión ASCII):
    
    Bash
    
    ```
    tshark -r shark-on-wire-2-capture.pcap -Y "udp.port == 22" -T fields -e udp.srcport | awk '{if($1>5000) printf "%c", $1-5000}' ; echo ""
    ```
    
- La ejecución del script extrajo exitosamente el texto oculto, revelando la bandera completa (que en esta variante del reto de la academia comienza con `academy{...}`).
```

## NOTAS ADICIONALES
- - **Esteganografía en red (Exfiltración):** Este reto demuestra cómo los atacantes pueden evadir firewalls y sistemas de detección de intrusos (IDS) incrustando información en las cabeceras de los protocolos de red (como el número de puerto) en lugar de enviar el texto en el cuerpo del paquete.
    
- **Tshark + Awk:** El uso combinado de `tshark` (la versión CLI de Wireshark) y `awk` (procesador de texto) es fundamental en el análisis forense digital para automatizar la extracción masiva de datos en capturas grandes. El comando `-T fields -e udp.srcport` es clave para aislar únicamente la columna de datos que nos interesa.

## REFERENCIAS
- - Reto original: **picoCTF 2019 / Cylab Academy** - Categoría: _Forensics_ (shark on wire 2).
    
- Documentación oficial de **Wireshark** (Filtros de visualización / Display Filters).
    
- Manual de **tshark** para extracción de campos de red.
    
- Tabla de codificación de caracteres **ASCII**.