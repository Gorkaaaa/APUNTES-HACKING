
# DENTRO DE LA MÁQUINA.
### COMPROBAR SI TIENE
```shell
sqlcmd -?
```

### LISTAR TODAS LAS BASES DE DATOS.
```shell
sqlcmd -U db_admin -P 'B1@hx31234567890' -S localhost -d streamio_backup -Q "SELECT name FROM master..sysdatabases;" #EN -d EL NOMBRE DE LA BASE DE DATOS.
```

### LISTAR TABLAS.
```shell
sqlcmd -U db_admin -P 'B1@hx31234567890' -S localhost -d streamio_backup -Q "SELECT name FROM streamio_backup..sysobjects WHERE xtype = 'U';" #EN -d EL NOMBRE DE LA BASE DE DATOS.
```

### LISTAR TODO EL CONTENIDO.
```shell
sqlcmd -U db_admin -P 'B1@hx31234567890' -S localhost -d streamio_backup -Q "SELECT * from users" #EN -d EL NOMBRE DE LA BASE DE DATOS.
```