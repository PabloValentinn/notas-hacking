
## DESCRIPCION
- In the last challenge, you mastered octal (base 8), decimal (base 10), and hexadecimal (base 16) numbers, but this vault door uses a different change of base as well as URL encoding! The source code for this vault is here: [VaultDoor5.java](https://challenge-files.cylabacademy.net/library/d085790fcd0c6bfae8d8e539ae372300b7da193466d0d499d4653621fc485a7c/VaultDoor5.java)

## SOLUCION
```

- Se analizó la consigna del reto correspondiente al quinto desafío de la serie _vault-door_ de ingeniería inversa en aplicaciones Java, el cual combina técnicas de codificación estándar: URL Encoding (Percent-Encoding) y Base64.
    
- Se descargó el archivo fuente `VaultDoor5.java` mediante el enlace provisto por la plataforma.
    
- Se examinó la lógica implementada en el método de validación `checkPassword`:
    
    Java
    
    ```
    public boolean checkPassword(String password) {
        String urlEncoded = urlEncode(password.getBytes());
        String base64Encoded = base64Encode(urlEncoded.getBytes());
        String expected = "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
                        + "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
                        + "JTM0JTVmJTY1JTMzJTMxJTM1JTMyJTYyJTY2JTM0";
        return base64Encoded.equals(expected);
    }
    ```
    
- **Análisis del Flujo de Transformación:**
    
    - El algoritmo toma la contraseña ingresada en texto plano y aplica un pipeline de dos etapas sucesivas:
        
        1. Codificación URL (_Percent-Encoding_) sobre los bytes originales, sustituyendo caracteres por su secuencia `%XX`.
            
        2. Codificación Base64 sobre la cadena resultante para producir una representación ASCII de 64 caracteres imprimibles.
            
    - El valor resultante se compara contra la constante concatenada `expected`.
        
- **Reversión del Pipeline:**
    
    - Dado que tanto Base64 como URL Encoding son esquemas de representación de datos y no funciones criptográficas de un solo sentido (hash), el proceso es estrictamente determinista y reversible.
        
    - Para reconstruir la contraseña original, se invirtió la secuencia de decodificación en orden inverso:
        
        $$\text{expected} \xrightarrow{\text{Base64 Decode}} \text{urlEncoded} \xrightarrow{\text{URL Decode}} \text{password}$$
        
    - Se implementó un script en Python para concatenar los fragmentos, decodificar el valor Base64 a una cadena de texto y desescapar los caracteres codificados por URL:
        
        Python
        
        ```
        import base64
        import urllib.parse
        
        expected = (
            "JTYzJTMwJTZlJTc2JTMzJTcyJTc0JTMxJTZlJTY3JTVm"
            "JTY2JTcyJTMwJTZkJTVmJTYyJTYxJTM1JTY1JTVmJTM2"
            "JTM0JTVmJTY1JTMzJTMxJTM1JTMyJTYyJTY2JTM0"
        )
        
        # 1. Decodificación Base64
        url_encoded = base64.b64decode(expected).decode("utf-8")
        print(f"[*] Intermedio URL Encoded: {url_encoded}")
        
        # 2. Decodificación URL (Percent-Decoding)
        password = urllib.parse.unquote(url_encoded)
        print(f"[+] Contraseña descifrada: {password}")
        print(f"[+] Bandera: academy{{{password}}}")
        ```
        

```
  - La decodificación intermedia de Base64 produjo la cadena con codificación porcentual:
    `%63%30%6e%76%33%72%74%31%6e%67%5f%66%72%30%6d%5f%62%61%35%65%5f%36%34%5f%65%33%31%35%32%62%66%34`
  - La resolución final de las secuencias hexadecimales URL reveló la contraseña:
    `c0nv3rt1ng_fr0m_ba5e_64_e3152bf4`
- Se estructuró la clave obtenida dentro del formato formal de la plataforma: `academy{c0nv3rt1ng_fr0m_ba5e_64_e3152bf4}` (o `picoCTF{c0nv3rt1ng_fr0m_ba5e_64_e3152bf4}`).



## NOTAS ADICIONALES
- Codificación vs. Cifrado en Control de Accesos: 1. **Diferenciación Fundamental:** Un error común en desarrollo de software consiste en confundir algoritmos de codificación (como Base64, Hexadecimal o URL Encode) con mecanismos de cifrado (*encryption*). Los métodos de codificación están diseñados exclusivamente para garantizar la interoperabilidad de datos a través de canales con restricciones de caracteres, pero no proporcionan confidencialidad alguna, ya que no dependen de una clave secreta. 2. **Seguridad en la Validación de Secretos:** Implementar validaciones encadenando múltiples capas de codificación estática constituye una forma frágil de "seguridad por oscuridad". En aplicaciones seguras, las contraseñas deben procesarse mediante funciones de derivación de claves criptográficamente robustas (KDF) con sal aleatoria (como PBKDF2, scrypt o Argon2) antes de almacenarse o verificarse.
## REFERENCIAS
- Reto original: picoCTF 2019 - Categoría: Reverse Engineering (Medium). - Autor: Mark E. Haase. - Conceptos aplicados: Ingeniería Inversa en Java, Decodificación Base64 (RFC 4648), Decodificación de URL / Percent-Encoding (RFC 3986), CWE-311 (Falta de Cifrado en Datos Sensibles).