#### Instalación
```python
pip install requests
```

#### Petición por GET basica
```python
import requests

resp = requests.get('https://www.google.com/')

print(resp.status_code)
```
Respuesta:
```bash
ASUS@DESKTOP-IABKB9U MINGW64 ~/Documents/Programación/python/req
$ python test.py
200
```

### Respuestas
Podemos modificar el print de la tercera linea para recibir solo las respuestas que nos interesen, **ejemplos**:

**HTML**
```python
print(resp.content)
```

**JSON**
```python
print(resp.JSON())
```



#### Petición GET un poco más avanzada
```python
import requests
response = requests.get('https://www.google.com/')

if response.status_code == 200:
    if 'application/json' in response.headers.get('Content-Type', ''):
        try: # Intenta dar la respuesta con json
            data = response.json() # En caso de que pueda dar la respuesta con python nos la da.
            print(data) # La muestra en consola.
        except requests.exceptions.JSONDecodeError as e: # Un manejo de erroes en caso de que no pueda decodificar el JSON, guarda el requests.exceptions.JSONDecodeError en la variable (e).
            print(f"Error decoding JSON: {e}") # Imprimir el error
    else:
        print("La respuesta no es JSON. Aquí está el contenido de la respuesta:") # Nos dice que no es JSON
        print(response.text[:1000])  # Muestra los primeros 1000 caracteres del contenido
else:
    print(f"Error: {response.status_code}") # En caso de que no sea 200 nos imprime el codigo de estado.
```

#### Petición por POST basica
```python
import requests

url = "http://httpbin.org/post"

data={
    "nombre":"ejemplo",
    "fecha":"2024"
}

requests.post(url,json=data)
```

#### Petición POST más avanzada
```python
import requests # Importar libreria
from requests.exceptions import HTTPError, Timeout, RequestException # Importar especificas

url = "http://httpbin.org/post" # URL
  
data = {
    "nombre": "ejemplo",
    "fecha": "2024"
} # Diccionario de datos que se envian por POST

headers = {
    "Content-Type": "application/json",
    "User-Agent": "mi-app/0.0.1"
} # Diccionario de cabezeras que se envian. 

try: # El try lo utilizamos para el manejo de excepciones
    response = requests.post(url, json=data, headers=headers, timeout=10) # El timeout 10 hace que la solicitud no espere más de 10s a la respuesta.
    response.raise_for_status() # Manejo de errores HTTP automatizado

    try:
        json_response = response.json() # Recoge la respuesta JSON
        print("JSON response:", json_response) # Imprime el JSON

    except ValueError:
        print("La respuesta no es JSON:", response.text) # Nos imprime una respuesta que no es JSON

# Manejo de errores especificos.
except HTTPError as http_err:
    print(f"HTTP error occurred: {http_err}")
except Timeout as timeout_err:
    print(f"Request timed out: {timeout_err}")
except RequestException as req_err:
    print(f"Request error occurred: {req_err}")
except Exception as err:
    print(f"An error occurred: {err}")
```