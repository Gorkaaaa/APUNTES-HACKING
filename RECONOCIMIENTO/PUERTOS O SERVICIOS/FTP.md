
### CONECTARSE COMO INVITADO
```shell
❯ ftp 10.10.10.103
	username:anonymoous
	password: 
```


### CONECTARSE POR NC
```r
[POR NC HACE FALTA ESCRIBER EL USER, PASS]
❯ nc 10.10.10.156 21
USER 8rOEkcLSHhVcpPasyTV23sT9p7pJemPv
PASS 8rOEkcLSHhVcpPasyTV23sT9p7pJemPv
```


### DESCARGAR TODO EL CONTENIDO DEL FTP
```R
prompt off
mget *
```