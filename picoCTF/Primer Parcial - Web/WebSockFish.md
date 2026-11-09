
## DESCRIPCION

- Can you win in a convincing manner against this chess bot? He won't go easy on you! You can find the challenge [here](http://xebec.cylabacademy.net:31942/).

## SOLUCION

```

- Se accedió a la aplicación web proporcionada por el reto, la cual consistía en un juego de ajedrez interactivo contra un bot (representado por un pez). Se observó que la aplicación utilizaba WebSockets para la comunicación en tiempo real entre el navegador (cliente) y el servidor.
    
- Se inspeccionó el código fuente de la página web utilizando las herramientas de desarrollador del navegador (F12). Se identificó una función JavaScript global llamada `sendMessage(message)`, la cual era utilizada por la aplicación para enviar los movimientos y el estado del juego al servidor a través del WebSocket.
    
- Se determinó que el servidor confiaba ciegamente en los datos enviados por el cliente sin realizar una validación adecuada. El servidor esperaba recibir mensajes con el formato `eval [puntuación]` para actualizar la evaluación del motor de ajedrez (Stockfish). Si la puntuación era inferior a un umbral predefinido (alrededor de -50000), el servidor declaraba la rendición del bot y revelaba la bandera.
    
- Se procedió a explotar la vulnerabilidad de confianza del lado del cliente (Client-Side Trust). Se abrió la consola de desarrollador del navegador (pestaña "Console") y se ejecutó la función `sendMessage` con un payload falso que simulaba una puntuación extremadamente negativa para el bot.
    
- Se ejecutó el siguiente comando en la consola:  
    `sendMessage("eval -1000000")`
    
- El servidor recibió el mensaje, lo procesó como una evaluación legítima del motor de ajedrez y, al detectar que la puntuación superaba el umbral de rendición, finalizó la partida declarando la victoria del jugador y devolvió la bandera (flag) en la respuesta.
    
- La bandera obtenida fue: `picoCTF{c1i3nt_s1d3_w3b_s0ck3t5_dc1dbff7}`.
```

## NOTAS ADICIONALES

- - **Client-Side Trust (Confianza en el Lado del Cliente):** Esta vulnerabilidad ocurre cuando una aplicación confía en datos críticos enviados por el cliente (como puntuaciones, estados de juego o precios) sin validarlos en el servidor. En este reto, el servidor confiaba en la puntuación del motor de ajedrez enviada por el navegador, lo que permitió al atacante falsificar una derrota del bot para obtener la bandera.
    
- **Manipulación de WebSockets:** Los WebSockets son un protocolo de comunicación bidireccional en tiempo real. Si la aplicación no valida los mensajes entrantes, un atacante puede inyectar mensajes falsos directamente desde la consola del navegador. La función `sendMessage` era global y accesible, lo que facilitó la explotación.
    
- **Impacto:** La explotación exitosa de esta vulnerabilidad permite a un atacante manipular el estado del juego, obtener victorias falsas o, en un escenario más grave, alterar datos sensibles del servidor. En este caso, el impacto se limitó a la obtención de la bandera del reto.
    
- **Prevención:** Para prevenir este tipo de vulnerabilidades, el servidor debe validar todos los datos críticos recibidos del cliente. En el caso de un juego de ajedrez, el servidor debería recalcular la puntuación basándose en el estado real del tablero y los movimientos válidos, en lugar de confiar en la puntuación enviada por el cliente. Además, se deben implementar mecanismos de autenticación y autorización para las conexiones WebSocket.

## REFERENCIAS
- - Reto original: picoCTF 2025 - Categoría: Web Exploitation (WebSockFish).
    
- Conceptos aplicados: Client-Side Trust, WebSocket Manipulation, JavaScript Console Exploitation, Input Validation Bypass, Remote Code Execution (RCE) indirecta.