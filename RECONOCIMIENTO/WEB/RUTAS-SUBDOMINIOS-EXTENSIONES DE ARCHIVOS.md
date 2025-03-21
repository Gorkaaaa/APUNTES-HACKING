
### CONECTARSE A UN IIS
```shell
cadaver http://192.168.205.122
```

### SUBDOMINIOS
```shell
#WFUZZ
❯ wfuzz -c -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -H "Host: FUZZ.pov.htb" -t 100 10.10.11.251

#EN BASE AL CODIGO FUENTE
curl -s http://dimension.worker.htb/#work | grep -oh 'http://.*worker.htb'
```


### RUTAS
```shell
#ENUMERACIÓN NORMAL
❯ wfuzz -c -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://internal.analysis.htb/FUZZ --hc=404 -t 200

#ENUMERACIÓN POR POST
❯ wfuzz --hh=31 -X POST -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u 'http://10.10.11.161/api/v1/user/FUZZ' -t 100

#WORDLIST IIS
❯ wfuzz -c --hc=404 -w /usr/share/wordlists/seclists/Discovery/Web-Content/IIS.fuzz.txt -u http://search.htb/FUZZ
```


### GENERAL
```shell
❯ dirsearch -u 'http://example.com'
```


### EXTENSIONES
```shell
❯ wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://internal.analysis.htb/users/FUZZ.php --hc=404 -t 200
```



### DOS FUZZS
```shell
❯ wfuzz -c --hc=404 -t 200 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -z list,txt-pdf-html -u "http://bethebest101.uk.htb/logs/e21cece511f43a5cb18d4932429915ed/FUZZ.FUZ2Z"
```



### PARAMETROS
```shell
❯ wfuzz -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u "http://internal.analysis.htb/users/list.php?FUZZ=test" --hc=404 -t 200 --hh=17
```



### HEADERS
```shell
# Wfuzz para headers, por ejemplo, nos advierten de que tenemos que entrar por una IP determinada pero no sabemmos que header usar, al buscar encontramos que hay muchos tipos de headers y decidimos probar con todos con:
wfuzz -c -t 100 -w headers.txt -u http://10.10.10.167/admin.php -H "FUZZ: 192.168.4.28"
```



### NÚMEROS
```shell
❯ wfuzz -c -t 200 --hh=7888 -z range,0000-9999 "http://10.10.11.173/reports.php?report=FUZZ"
```



### PLUGINS WORDPRESS
```shell
❯ wfuzz -c --hc=404 -t 200 -w /usr/share/SecLists/Discovery/Web-Content/CMS/wp-plugins.fuzz.txt -u http://192.168.234.77/webservices/wp/FUZZ
```




