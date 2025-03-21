

# IDENTIFICAR PERMISOS SOBRE EL DOCKER
### SUDO -L
```shell
noah@thenotebook:~$ sudo -l
(ALL) NOPASSWD: /usr/bin/docker exec -it webapp-dev01*
```

# EJECUCUÓN DE COMANDOS COMO ADMINISTRADOR
**RCE**
```shell
noah@thenotebook:~$ sudo /usr/bin/docker exec -it webapp-dev01 bash
root@0f4c2517af40:/opt/webapp# whoami
root
```