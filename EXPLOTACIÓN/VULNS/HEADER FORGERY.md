
### 1. IDENTIFICACIÓN DEL HEADER
```shell
❯ wfuzz -c -w /usr/share/seclists/Miscellaneous/web/http-request-headers/http-request-headers-fields-large.txt -H "FUZZ : 192.168.4.28" -u http://10.10.10.167/admin.php --hh=89
```

### 2. CONFIGURAR EL HEADER X-Forwarded-FOR
```shell
BurpSuite > ProxyConfig > Proxy > Match And Replace Rules > Replace => X-Forwarded-FOR:IP
```



