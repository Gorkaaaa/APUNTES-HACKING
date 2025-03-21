
# PONERTE EN ESCUCHA
```shell
#CAMBIAR LA INTERFAZ DE RED
tcpdump -i tun0 icmp -n
```

# CAPTURAR PAQUETES CON TCP DUMP EN MÁQUINA VICTIMA
```shell
#PONER LA INTERFAZ DE RED DE LA MÁQUINA
tcpdump -i docker0 -w Captura.cap -v
```