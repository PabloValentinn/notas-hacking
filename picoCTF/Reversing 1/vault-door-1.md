
## DESCRIPCION
- This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: [VaultDoor1.java](https://challenge-files.cylabacademy.net/library/7459f4a2a283307f76c6bf1b035e6f99a63123c791891ddaeb97ade552711f22/VaultDoor1.java)
## SOLUCION
```

- Se analizó la consigna del reto correspondiente al segundo nivel de la serie de ingeniería inversa centrada en aplicaciones Java.
    
- Se descargó el archivo fuente `VaultDoor1.java` proporcionado mediante el enlace del reto.
    
- Se examinó el código fuente dentro del entorno de terminal:
    
    Bash
    
    ```
    cat VaultDoor1.java
    ```
    
- **Análisis Estático del Código:**
    
    - El método principal toma la contraseña introducida por el usuario, descarta el envoltorio exterior del formato de bandera y envía la cadena resultante al método de verificación `checkPassword(String password)`.
        
    - En `checkPassword`, se valida que la longitud de la cadena sea de 32 caracteres (`password.length() == 32`) y se compara cada posición de forma individual mediante `password.charAt(index) == 'char'`, pero con los índices intencionalmente desordenados para dificultar su lectura lineal:
        
        Java
        
        ```
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == '3' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               ...
        ```
        
- **Reconstrucción y Automatización:**
    
    - Se desarrolló un script en Python para extraer todas las parejas `(índice, carácter)` utilizando expresiones regulares, ordenar la secuencia de acuerdo con sus índices numéricos de 0 a 31 y concatenar los caracteres:
        
        Python
        
        ```
        import re
        
        with open("VaultDoor1.java") as f:
          content = f.read()
        
        # Extracción de pares (índice, carácter)
        matches = re.findall(
            r"charAt\s*\(\s*(\d+)\s*\)\s*==\s*[\x27\"](.)[\x27\"]", content
        )
        
        # Ordenar por índice ascendente (0 a 31)
        ordered = sorted([(int(idx), ch) for idx, ch in matches], key=lambda x: x[0])
        flag_content = "".join(ch for idx, ch in ordered)
        
        print(f"academy{{{flag_content}}}")
        ```
        

```
  - También se pudo resolver directamente desde la línea de comandos de Linux ordenando las líneas numéricamente por el contenido del paréntesis:
    ```bash
    grep "charAt" VaultDoor1.java | sort -n -k2 -t'(' | awk -F"'" '{printf "%s", $2}' && echo ""
    ```
  - La reconstrucción ordenada de los 32 caracteres reveló la frase: `d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0` (*"descramble the characters"*).
- Se encapsuló la cadena resultante dentro del formato formal de la plataforma: `academy{d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0}` (o `picoCTF{d35cr4mbl3_tH3_cH4r4cT3r5_ff63b0}`).


## NOTAS ADICIONALES
- Ofuscación por Desordenamiento de Índices (*Character Scrambling*): 1. **Mecanismo de Verificación:** Al fragmentar la comparación de cadenas en evaluaciones booleanas individuales evaluadas con cortocircuito (`&&`), el desarrollador intenta evadir la simple inspección de cadenas legibles (*strings inspection*). Sin embargo, al seguir siendo comparaciones estáticas directas, el flujo es completamente reversible mediante análisis léxico o scripts de ordenamiento. 2. **Buenas Prácticas Criptográficas:** Las contraseñas nunca deben verificarse carácter por carácter de forma explícita ni secuencial en el código fuente, ya que esto además introduce vulnerabilidades de canal lateral basadas en tiempo (*timing attacks*), donde un atacante puede deducir caracteres válidos midiendo la latencia de respuesta del procesador. **REFERENCIAS**
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Medium).
- Autor: Mark E. Haase. 
- Conceptos aplicados: Ingeniería Inversa en Java, Análisis Estático de Código Fuente, Procesamiento y Extracción con Regex en Python, Manejo de Índices en Cadenas.