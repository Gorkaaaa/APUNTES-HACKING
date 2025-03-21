
### ENUMERAR INFORMACIÓN DE USUARIOS ELIMINADOS
```shell
Get-ADObject -ldapfilter "(&(isDeleted=TRUE))" -IncludeDeletedObjects
```

### CON FILTROS
```shell
Get-ADObject -ldapfilter "(&(objectclass=user)(isDeleted=TRUE))" -IncludeDeletedObjects
```

### FILTRAR POR UN USUARIO
```shell
Get-ADObject -ldapfilter "(&(objectclass=user)(DisplayName=TempAdmin)(isDeleted=TRUE))" -IncludeDeletedObjects -Properties *
```