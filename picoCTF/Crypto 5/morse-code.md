

## DESCRIPCION
  - Morse code is well known. Can you decrypt this? Download the file [here](https://challenge-files.cylabacademy.net/library/3728bfa4e8314fddd6b7e9f3fae9cb453b459a0bd4b3a29a9224701152f0cd89/morse_chal.wav).

Wrap your answer with academy{}, put underscores in place of pauses, and use all uppercase.

## SOLUCION
```
- Se descargó el archivo de audio adjunto denominado `morse_chal.wav` provisto a través del enlace del reto.
    
- Se identificó que el archivo contenía una señal de modulación por tono de onda continua (_Continuous Wave_ / CW) correspondiente al estándar internacional de **Código Morse** acústico.
    
- Se procesó el archivo de audio mediante un decodificador de frecuencias adaptativo para aislar la onda portadora y transcribir las secuencias de pulsos elementales (puntos `.` y rayas `-`):
    
    - `.--` / `....` / `....-` / `--...` $\rightarrow$ **WH47**
        
    - `....` / `....-` / `--...` / `....` $\rightarrow$ **H47H**
        
    - `----.` / `-----` / `-..` $\rightarrow$ **90D**
        
    - `.--` / `..---` / `-----` / `..-` / `----.` / `....` / `--...` $\rightarrow$ **W20U9H7**
        
- El mensaje transcrito reveló la frase: `WH47 H47H 90D W20U9H7` (alusión en _leetspeak_ al mensaje bíblico _"What hath God wrought"_, enviado por Samuel Morse en la inauguración de la primera línea de telégrafo oficial en 1844).
    
- Se aplicaron las directrices de formateo exigidas en la descripción del reto: sustitución de las pausas/espacios entre palabras por guiones bajos (`_`), preservación de mayúsculas y encapsulación dentro del prefijo `academy{}`.
    
- La bandera final obtenida fue: `academy{WH47_H47H_90D_W20U9H7}`.

```
## NOTAS ADICIONALES
- Código Morse y Procesamiento de Señales de Audio:

1. **Estructura Temporal del Código Morse:** El código se rige por relaciones de duración estandarizadas: una raya equivale a tres puntos; la separación entre elementos de una misma letra es de un punto; el espacio entre letras es de tres puntos; y la pausa entre palabras completas equivale a siete puntos.
    
2. **Decodificación Computacional vs. Filtro de Audio:** Analizar código Morse a partir de datos binarios brutos (PCM) requiere filtrar la frecuencia portadora dominante (habitualmente entre 600 Hz y 800 Hz) para evitar que armónicos, variaciones de volumen o ruidos transitorios sean interpretados erróneamente como pulsos telegráficos breves.

## REFERENCIAS
- Reto original: picoCTF 2022 - Categoría: Cryptography (Medium).
    
- Conceptos aplicados: Código Morse Internacional (Audio/CW), Análisis de Señales de Audio, Formato Leetspeak, Historia de las Telecomunicaciones.