
### CON PYTHON
```python
❯ pip3 install pyaes --break-system-packages

#CODE
import pyaes
from base64 import b64decode
key = b"c4scadek3y654321" [PASSWORD]
iv = b"1tdyjCbY1Ix49842" [IV]
aes = pyaes.AESModeOfOperationCBC(key, iv = iv) 
decrypted = aes.decrypt(b64decode('BQO5l5Kj9MdErXx6Q6AGOw=='))
print(decrypted.decode())

```