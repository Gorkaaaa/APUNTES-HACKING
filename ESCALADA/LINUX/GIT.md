


**ENUMERACIÓN DE UN PROYECTO GIT WEB.**
```r
❯ git clone https://github.com/arthaud/git-dumper
❯ pip3 install -r requirements.txt --break-system-packages
❯ python3 git_dumper.py http://blog-dev.travel.htb/.git/ ../project
```

**UNA VEZ EL PROEYCTO COPIADO PODEMOS VER LAS ULTIMAS VERSIONES DEL PROYECTO...**
```r
❯ git log
❯ git show ID
```

### LISTAR ARCHIVOS GIT
```shell
roy@zetta:/$ find \-name .git 2>/dev/null
```

### ENUMERAR LOGS
```shell
developer@ambassador:/opt/my-app$ git log
```

### CONTENIDO DE UN LOG
```shell
developer@ambassador:/opt/my-app$ git show 33a53ef9a207976d5ceceddc41a199558843bf3c
```