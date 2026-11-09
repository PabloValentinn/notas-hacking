
## DESCRIPCION
- This vault uses ASCII encoding for the password. The source code for this vault is here: [VaultDoor4.java](https://challenge-files.cylabacademy.net/library/765fe2e27bfd01f2fc3432d711fedd1ef1103879d9bfff0302de118737fa4d0c/VaultDoor4.java)

## SOLUCION
```
- Se analizó la consigna del reto correspondiente al cuarto desafío de la serie de ingeniería inversa en aplicaciones Java, el cual se enfoca en la interpretación de arreglos de bytes y la representación de caracteres bajo distintos sistemas de codificación numérica y posicional.
    
- Se descargó el archivo fuente `VaultDoor4.java` mediante el enlace provisto por la plataforma.
    
- Se inspeccionó el método de validación `checkPassword` en el código fuente:
    
    Java
    
    ```
    public boolean checkPassword(String password) {
        byte[] passBytes = password.getBytes();
        byte[] myBytes = {
            106 , 85  , 53  , 116 , 95  , 52  , 95  , 98  ,
            0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f,
            0142, 0131, 0164, 063 , 0163, 0137, 0143, 061 ,
            '9' , '4' , 'e' , '1' , '8' , '5' , '1' , 'e' ,
        };
        for (int i=0; i<32; i++) {
            if (passBytes[i] != myBytes[i]) {
                return false;
            }
        }
        return true;
    }
    ```
    
- **Análisis de las Codificaciones Numéricas en Java:**
    
    - El método toma la cadena introducida por el usuario, obtiene sus bytes directos (`password.getBytes()`) y realiza una comparación posicional de 32 elementos contra el arreglo estático `myBytes`.
        
    - El arreglo `myBytes` divide los 32 caracteres en cuatro bloques de 8 elementos, empleando cuatro convenciones sintácticas diferentes de representación de enteros y literales en Java:
        
        1. **Decimal (Base 10):** Representación estándar sin prefijos (`106, 85, 53, 116, 95, 52, 95, 98`) $\rightarrow$ `'j'`, `'U'`, `'5'`, `'t'`, `'_'`, `'4'`, `'_'`, `'b'` (`jU5t_4_b`).
            
        2. **Hexadecimal (Base 16):** Enteros delimitados por el prefijo `0x` (`0x55, 0x6e, 0x43, 0x68, 0x5f, 0x30, 0x66, 0x5f`) $\rightarrow$ `'U'`, `'n'`, `'C'`, `'h'`, `'_'`, `'0'`, `'f'`, `'_'` (`UnCh_0f_`).
            
        3. **Octal (Base 8):** En la especificación del lenguaje Java, los literales enteros que inician con el dígito `0` se interpretan en base 8 (`0142, 0131, 0164, 063, 0163, 0137, 0143, 061`) $\rightarrow$ `'b'`, `'Y'`, `'t'`, `'3'`, `'s'`, `'_'`, `'c'`, `'1'` (`bYt3s_c1`).
            
        4. **Caracteres ASCII Literales:** Valores asignados directamente entre comillas simples (`'9', '4', 'e', '1', '8', '5', '1', 'e'`) $\rightarrow$ `94e1851e`.
            
- **Automatización y Reconstrucción en Python:**
    
    - Se implementó un script que extrae el arreglo desde `VaultDoor4.java`, procesa la base numérica adecuada para cada token y decodifica la contraseña completa:
        
        Python
        
        ```
        import re
        
        content = open("VaultDoor4.java").read()
        raw_array = re.search(r"myBytes\s*=\s*\{([^}]+)\}", content).group(1)
        tokens = [
            tok.strip()
            for tok in raw_array.replace("\n", " ").split(",")
            if tok.strip()
        ]
        
        
        def decode_token(tok):
          if tok.startswith("'") and tok.endswith("'"):
            return ord(tok[1:-1])
          elif tok.startswith("0x") or tok.startswith("0X"):
            return int(tok, 16)
          elif tok.startswith("0") and len(tok) > 1 and tok[1].isdigit():
            return int(tok, 8)
          return int(tok, 10)
        
        
        password = "".join(chr(decode_token(t)) for t in tokens)
        print(f"academy{{{password}}}")
        ```
        

```
  - La concatenación de las cuatro secciones reveló la frase en texto claro: `jU5t_4_bUnCh_0f_bYt3s_c194e1851e`.
- Se encapsuló la contraseña descifrada dentro del formato formal de la plataforma

## NOTAS ADICIONALES
- Sistemas de Representación Numérica y Análisis Estático: 1. **Peculiaridades de Literales en Java y C/C++:** La convención histórica de prefijar números con un `0` para denotar base octal suele generar interpretaciones erróneas durante el análisis visual directo si se asumen como números decimales con relleno de ceros (*zero-padded decimals*). Comprender las reglas léxicas de los compiladores es indispensable para el análisis estático riguroso. 2. **Evaluación de Complejidad:** Aunque la variedad de bases ofusca la legibilidad inmediata del código ante un analista novato, a nivel de compilación todos los valores se reducen a constantes de un solo byte en la tabla de constantes del archivo `.class` (*constant pool* / instrucciones `bipush`), permitiendo una resolución directa mediante desensamblado o scripting.

## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Medium).
- Autor: Mark E. Haase. 
- Conceptos aplicados: Ingeniería Inversa en Java, Sistemas de Numeración (Decimal, Hexadecimal, Octal), Tabla de Códigos ASCII, Extracción de Literales en Python.