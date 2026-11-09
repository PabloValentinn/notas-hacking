

## DESCRIPCION
- A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.

To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!

Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.cylabacademy.net/library/88815ae7a4641c35f494d4d4b56e618428fe5cfb6a8b47c7a600eb98d670a72b/myNetworkTraffic.pcap) and try to get the flag.

## SOLUCION
```

- Se analizó la descripción del desafío, la cual indicaba la necesidad de inspeccionar tráfico de red contenido en un archivo de captura de paquetes (PCAP).
    
- Se descargó el archivo `myNetworkTraffic.pcap` en el entorno de análisis de Kali Linux.
    
- Inicialmente se inspeccionó el archivo de forma gráfica utilizando `Wireshark`. El análisis inicial reveló una anomalía en el protocolo TCP: el atacante estaba exfiltrando datos al inyectar pequeñas cargas útiles (payloads) de texto dentro de paquetes con la bandera de sincronización `[SYN]` habilitada, los cuales bajo un estándar de red normal no deberían contener datos de usuario.
    
- Para agilizar la extracción de los datos fragmentados sin tener que inspeccionar los paquetes uno por uno, se utilizó la herramienta de terminal `strings` ejecutando el comando `strings myNetworkTraffic.pcap`.
    
- El volcado de texto en la consola reveló múltiples cadenas ofuscadas en formato Base64. Cada segmento enviado por el atacante contenía un sufijo de relleno (como `gq`).
    
- Se procedió a limpiar el texto extraído y aislar las cadenas Base64 válidas descartando los falsos positivos.
    
- Al decodificar y ordenar lógicamente los fragmentos extraídos, se reconstruyó el texto en claro, obteniendo exitosamente la bandera robada: `academy{1t_w4snt_th4t_34sy_tbh_4r_dd2075f0}`
```

## NOTAS ADICIONALES
- Exfiltración de Datos (Data Exfiltration): Los atacantes modernos evitan enviar grandes bloques de datos robados porque los sistemas de detección de intrusos (IDS) y firewalls lo detectarían inmediatamente por el volumen anómalo. En su lugar, utilizan técnicas de "contrabando" fragmentando el archivo o el texto sensible y enviándolo pieza por pieza, a menudo oculto en las cabeceras de protocolos legítimos (como peticiones DNS, o en este caso, "saludos" TCP SYN). El uso combinado de decodificadores (Base64), analizadores de protocolos (Wireshark) y extractores rápidos de texto (Strings) es vital en la respuesta a incidentes (Blue Team) para reconstruir qué fue exactamente lo que el atacante logró robar de la red.

## REFERENCIAS
- Reto original: picoCTF 2025 - Categoría: Forensics (Easy).
    
- Conceptos aplicados: Packet Capture (PCAP), Exfiltración de Datos Fragmentados, Análisis con Wireshark, Extracción de Strings en Terminal, Decodificación Base64.