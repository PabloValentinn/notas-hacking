
## DESCRIPCION

- This vault uses for-loops and byte arrays. The source code for this vault is here: [VaultDoor3.java](https://challenge-files.cylabacademy.net/library/14bca593f597cbc6b521a3deb17bd94a81c603c8cdc801f0a6b41f89ec79e27f/VaultDoor3.java)
## SOLUCION
```

- Se analizó la consigna del desafío correspondiente al tercer nivel de la serie de retos de ingeniería inversa en Java, enfocado en permutaciones estructuradas sobre arreglos de caracteres mediante estructuras cíclicas (`for`).
    
- Se descargó el archivo fuente `VaultDoor3.java` utilizando el enlace provisto por la plataforma.
    
- Se inspeccionó la implementación del método de validación `checkPassword` en el código fuente:
    
    Java
    
    ```
    public boolean checkPassword(String password) {
        if (password.length() != 32) {
            return false;
        }
        char[] buffer = new char[32];
        int i;
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm18g947_u_4_m9r54f");
    }
    ```
    
- **Análisis del Algoritmo de Transposición:**
    
    - El método comprueba que la cadena ingresada tenga exactamente 32 caracteres de longitud.
        
    - Genera un arreglo de caracteres intermedio `buffer` de 32 posiciones y reubica los caracteres de la contraseña de entrada `password` según cuatro transformaciones sucesivas:
        
        1. Del índice 0 al 7: Copia directa sin alteración posicional (`buffer[i] = password[i]`).
            
        2. Del índice 8 al 15: Invierte el bloque (`buffer[i] = password[23 - i]`).
            
        3. Del índice 16 al 30 (en pasos pares): Asigna caracteres en orden decreciente (`buffer[i] = password[46 - i]`).
            
        4. Del índice 31 al 17 (en pasos impares decrementales): Conserva las posiciones impares directas (`buffer[i] = password[i]`).
            
    - La cadena resultante `buffer` se compara contra la cadena de referencia `"jU5t_a_sna_3lpm18g947_u_4_m9r54f"`.
        
- **Reversión del Algoritmo:**
    
    - Al ser una biyección (permutación uno a uno), el proceso inverso consiste en ubicar cada elemento de la cadena objetivo en la posición original que le dio origen:
        
        - Para $0 \le i < 8$: `password[i] = buffer[i]`
            
        - Para $8 \le i < 16$: `password[23 - i] = buffer[i]`
            
        - Para $16 \le i < 32$ con paso 2: `password[46 - i] = buffer[i]`
            
        - Para $31 \ge i \ge 17$ con decremento 2: `password[i] = buffer[i]`
            
    - Se implementó un script en Python para invertir el proceso automáticamente:
        
        Python
        
        ```
        target = "jU5t_a_sna_3lpm18g947_u_4_m9r54f"
        pw = [""] * 32
        
        for i in range(8):
          pw[i] = target[i]
        for i in range(8, 16):
          pw[23 - i] = target[i]
        for i in range(16, 32, 2):
          pw[46 - i] = target[i]
        for i in range(31, 16, -2):
          pw[i] = target[i]
        
        password = "".join(pw)
        print(f"academy{{{password}}}")
        ```
        

```
  - La ejecución reconstituyó la frase en texto plano: `jU5t_a_s1mpl3_an4gr4m_4_u_79958f`.
- Se encapsuló la contraseña en el formato formal requerido: `academy{jU5t_a_s1mpl3_
```
```

## NOTAS ADICIONALES
- Permutaciones y Funciones Biyectivas en Ingeniería Inversa: 1. **Reversibilidad Matemática:** Las permutaciones de índices operan como sustituciones posicionales que no destruyen información. Debido a esto, si se conoce el arreglo de salida y las reglas algebraicas de dispersión, es posible computar la función inversa directa sin requerir ataques de fuerza bruta ni análisis heurístico. 2. **Ofuscación de Cadenas por Anagramas:** Este tipo de lógica representa una técnica elemental de ofuscación de cadenas (*string scrambling*) orientada a evitar que cadenas legibles sean localizadas mediante utilidades estáticas como `strings` o desensambladores simples. No obstante, al residir toda la lógica en el propio binario sin interacción criptográfica asimétrica o hashing irreversible, el flujo permanece totalmente vulnerable frente a un análisis estático de código.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Medium). - Autor: Mark E. Haase. - Conceptos aplicados: Análisis Estático de Código Java, Reversión de Algoritmos de Transposición, Permutaciones en Arreglos de Bytes y Cadenas.