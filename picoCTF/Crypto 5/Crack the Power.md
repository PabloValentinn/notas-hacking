
## DESCRIPCION
- We received an encrypted message. The modulus is built from primes large enough that factoring them isn’t an option, at least not today. See if you can make sense of the numbers and reveal the flag. Download the [message](https://challenge-files.cylabacademy.net/library/f688af3e0e10229b8e2533aeb1f2b70c566d6fbae5f7c0cce8374ad3c4d86651/message.txt).

## SOLUCION
```

- Se examinó el archivo provisto `message.txt`, el cual contenía los parámetros de un cifrado asimétrico RSA: un módulo $N$ de tamaño superior a 4096 bits, un exponente de cifrado $e = 20$ y el texto cifrado $c$.
    
- **Criptoanálisis del ataque (Small Exponent / No Padding):** La operación de cifrado de RSA se define como:
    
    $$c \equiv m^e \pmod N$$
    
    Cuando el mensaje $m$ es corto (longitud de una bandera estándar) y no cuenta con esquemas de relleno criptográfico (_padding_ como PKCS#1 v1.5 o OAEP), al ser elevado al exponente público se cumple que:
    
    $$m^e < N$$
    
    Al cumplirse esta desigualdad, la operación módulo $N$ nunca desborda ni altera el resultado aritmético ($c = m^e$). En consecuencia, el texto cifrado $c$ es una potencia exacta de grado $e$ en el cuerpo de los números enteros reales, eliminando la necesidad de factorizar el módulo $N$ o conocer la clave privada $d$.
    
- Se implementó un algoritmo en Python utilizando búsqueda binaria sobre números enteros de precisión arbitraria para calcular la raíz $e$-ésima exacta de $c$ ($\sqrt[20]{c}$):
    
    Python
    
    ```
    def integer_nth_root(c, e):
        low, high = 0, c
        while low <= high:
            mid = (low + high) // 2
            p = mid**e
            if p == c:
                return mid, True
            elif p < c:
                low = mid + 1
            else:
                high = mid - 1
        return high, False
    
    
    # Extracción y cálculo directo
    e = 20
    c = 36350572406033754592040662295533368221856010815659718897671994991058237194687245443254984460129942431471259320396388467899827506839465701886747167028999692566835051584740156685199098155449031805453675064955700282036016386503389826387146193511170304982705618973753663438565871805117891358645466607362627924137805879978927778179053612174702933011812428247897869179383080325242210555648201357278551405053147815378060129847202236528589669509932554913321811048492060218106407800949520698994511710497077549426631416489722011410713845739170016582817678818006332440211821411946757819460040898994151850305119705272258876929600736846546916039620785315762174730157208868839652008589979863202820705814203918219495093961320166447307192007347810134027544622225737407972752512394741535241399073426149704540885715575924473403234549653523705347683585845535106453708977010270542980290095257800258741882460701455004838391546476714942044625973540115888984242959382679502077114929723477501983210878900844847755039910986478217513770166381539995445913879425692533450772913200337113169214988555844472102474517551637637914056566146688758107565206598273007415762362216730001
    m, _ = integer_nth_root(c, e)
    
    # Decodificación de entero a ASCII
    flag = m.to_bytes((m.bit_length() + 7) // 8, byteorder="big").decode("utf-8")
    print(flag)
    ```
```

## NOTAS ADICIONALES
- Fallo de Implementación en RSA de Libro de Texto (*Textbook RSA*): Este fallo demuestra por qué nunca se debe utilizar RSA puro sin esquemas de relleno determinista o probabilístico (como OAEP). Aunque el módulo $N$ sea inmenso y matemáticamente inexpugnable por factorización, la relación algebraica simple permite que un atacante revierta la operación matemática en tiempo logarítmico mediante aproximaciones numéricas o raíces directas, invalidando por completo la confidencialidad del mensaje.

## REFERENCIAS
- Reto original: picoMini by CMU-Africa - Categoría: Cryptography (Medium)[cite: 8]. 
- Conceptos aplicados: RSA sin Relleno (Unpadded RSA), Ataque de Exponente Pequeño (Small Public Exponent Attack), Raíz Entera Arbitraria.