

# .Crypt

### DESENCRIPTAR CON CLAVE PUBLICA, .CTYPT
```python
#!/usr/bin/python3
from Crypto.PublicKey import RSA
from pwn import *

f = open("decoder.pub", "r")

key = RSA.importKey(f.read())

log.info("n: %s" % key.n)
log.info("e: %s" % key.e)
```

```SHELL
❯ python3 dec.py
[*] n: 85161183100445121230463008656121855194098040675901982832345153586114585729131
[*] e: 65537
```

```shell
#FACTORIZAR EL NUMERO
https://factordb.com/
```

```python
#!/usr/bin/python3
from Crypto.PublicKey import RSA
from pwn import *
f = open("decoder.pub", "r")
key = RSA.importKey(f.read())
n = key.n
e = key.e
p = 280651103481631199181053614640888768819
q = 303441468941236417171803802700358403049
log.info("n: %s" % key.n)
log.info("p: %s" % p)
log.info("q: %s" % q)
log.info("e: %s" % key.e)
def egcd(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)
def modinv(a, m):
    g, x, y = egcd(a, m)
    if g != 1:
        raise Exception('null')
    else:
        return x % m
m = n-(p+q-1)
d = modinv(e,m)
log.info("m: %s" % m)
log.info("d: %s" % d)
finalKey = RSA.construct((n, e, d, p, q))
print("\n")
print(finalKey.exportKey().decode())
```

```shell
❯ python3 dec.py
[*] n: 85161183100445121230463008656121855194098040675901982832345153586114585729131
[*] p: 280651103481631199181053614640888768819
[*] q: 303441468941236417171803802700358403049
[*] e: 65537
[*] m: 85161183100445121230463008656121855193513948103479115215992296168773338557264
[*] d: 21250987814893564133283367312544315727523797355452606165102736035279600512161


-----BEGIN RSA PRIVATE KEY-----
MIGsAgEAAiEAvEeFgY9UxibHe/Mls88ARrXQ0RNetXeYj3AmLOYUmGsCAwEAAQIg
LvuiAxyjSPcwXGvmgqIrLQxWT1SAKVZwewy/gpO2bKECEQDTI2+4s2LacjlWAWZA
A2kzAhEA5Eizfe3idizLLBr0vsjD6QIRALlM92clYJOQ/csCjWeO1ssCEQDHxRNG
BVGjRsm5XBGHj1tZAhEAkJAmnUZ7ivTvKY17SIkqPQ==
-----END RSA PRIVATE KEY-----
```

```shell
❯ openssl rsault -decrypt -inkey id_rsa < pass.crypt
❯ openssl rsautl -decrypt -inkey id_rsa < pass.crypt
The command rsautl was deprecated in version 3.0. Use 'pkeyutl' instead.
nevermindthebollocks
```

```python
import requests
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP
from pwn import log
import sys

# --- Función para leer la clave pública ---
def read_public_key(filepath):
    with open(filepath, "r") as f:
        key = RSA.importKey(f.read())
    log.info("n: %s" % key.n)
    log.info("e: %s" % key.e)
    return key

# --- Función para factorizar n usando factordb ---
def factorize_n(n):
    log.info("Factorizando n en factordb...")
    url = f"https://factordb.com/api?query={n}"
    response = requests.get(url).json()
    if response['status'] != "FF":
        log.error("No se pudo factorizar n. Verifica en https://factordb.com/")
        sys.exit(1)
    factors = response['factors']
    p, q = int(factors[0][0]), int(factors[1][0])
    log.info("p: %s" % p)
    log.info("q: %s" % q)
    return p, q

# --- Funciones auxiliares para RSA ---
def egcd(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

def modinv(a, m):
    g, x, _ = egcd(a, m)
    if g != 1:
        raise Exception("No modular inverse")
    return x % m

# --- Construcción de la clave privada ---
def construct_private_key(n, e, p, q):
    m = (p - 1) * (q - 1)
    d = modinv(e, m)
    log.info("m: %s" % m)
    log.info("d: %s" % d)
    private_key = RSA.construct((n, e, d, p, q))
    log.info("Clave privada generada correctamente.")
    return private_key

# --- Desencriptar el archivo ---
def decrypt_file(private_key, filepath):
    with open(filepath, "rb") as f:
        encrypted_data = f.read()
    cipher = PKCS1_OAEP.new(private_key)
    decrypted_data = cipher.decrypt(encrypted_data)
    log.info("Archivo desencriptado correctamente.")
    return decrypted_data

# --- Proceso principal ---
def main():
    decoder_pub_file = input("Introduce la ruta del archivo con la clave pública (decoder.pub): ").strip()
    crypt_file = input("Introduce la ruta del archivo encriptado (pass.crypt): ").strip()

    log.info("Leyendo la clave pública...")
    public_key = read_public_key(decoder_pub_file)

    log.info("Factorizando n...")
    p, q = factorize_n(public_key.n)

    log.info("Construyendo la clave privada...")
    private_key = construct_private_key(public_key.n, public_key.e, p, q)

    log.info("Desencriptando el archivo...")
    decrypted_data = decrypt_file(private_key, crypt_file)

    log.success("Datos desencriptados: %s" % decrypted_data.decode())

if __name__ == "__main__":
    main()

```