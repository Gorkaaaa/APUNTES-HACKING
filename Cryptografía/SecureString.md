
# 1
```shell
[CONTENIDO A DESCRIFRAR]
www-data@fulcrum:~/uploads$ cat Fulcrum_Upload_to_Corp.ps1
cat Fulcrum_Upload_to_Corp.ps1
# TODO: Forward the PowerShell remoting port to the external interface
# Password is now encrypted \o/

$1 = 'WebUser'
$2 = '77,52,110,103,63,109,63,110,116,80,97,53,53,77,52,110,103,63,109,63,110,116,80,97,53,53,48,48,48,48,48,48' -split ','
$3 = '76492d1116743f0423413b16050a5345MgB8AEQAVABpAHoAWgBvAFUALwBXAHEAcABKAFoAQQBNAGEARgArAGYAVgBGAGcAPQA9AHwAOQAwADgANwAxADIAZgA1ADgANwBiADIAYQBjADgAZQAzAGYAOQBkADgANQAzADcAMQA3AGYAOQBhADMAZQAxAGQAYwA2AGIANQA3ADUAYQA1ADUAMwA2ADgAMgBmADUAZgA3AGQAMwA4AGQAOAA2ADIAMgAzAGIAYgAxADMANAA=' 
$4 = $3 | ConvertTo-SecureString -key $2
$5 = New-Object System.Management.Automation.PSCredential ($1, $4)

Invoke-Command -Computer upload.fulcrum.local -Credential $5 -File Data.ps1



[NOS ABRIMOS UNA POWERSHELL EN NUESTRO ORDENADOR Y PONEMOS EL CONTENIDO DEL ARCHIVO MÁS DOS FUNCIONES.]
PS C:\Users\user> $1 = 'WebUser'
PS C:\Users\user> $2 = '77,52,110,103,63,109,63,110,116,80,97,53,53,77,52,110,103,63,109,63,110,116,80,97,53,53,48,48,48,48,48,48' -split ','
PS C:\Users\user> $3 = '76492d1116743f0423413b16050a5345MgB8AEQAVABpAHoAWgBvAFUALwBXAHEAcABKAFoAQQBNAGEARgArAGYAVgBGAGcAPQA9AHwAOQAwADgANwAxADIAZgA1ADgANwBiADIAYQBjADgAZQAzAGYAOQBkADgANQAzADcAMQA3AGYAOQBhADMAZQAxAGQAYwA2AGIANQA3ADUAYQA1ADUAMwA2ADgAMgBmADUAZgA3AGQAMwA4AGQAOAA2ADIAMgAzAGIAYgAxADMANAA='
PS C:\Users\user> $4 = $3 | ConvertTo-SecureString -key $2
PS C:\Users\user> $5 = New-Object System.Management.Automation.PSCredential ($1, $4)
PS C:\Users\user> $Ptr = [System.Runtime.InteropServices.Marshal]::SecureStringToCoTaskMemUnicode($4)
PS C:\Users\user> $result = [System.Runtime.InteropServices.Marshal]::PtrToStringUni($Ptr)
PS C:\Users\user> [System.Runtime.InteropServices.Marshal]::ZeroFreeCoTaskMemUnicode($Ptr)
PS C:\Users\user> $result
M4ng£m£ntPa55
```

# 2
```shell
$s = cat .\admin-pass.xml
$ss = ConvertTo-SecureString $s
$cred = New-Object System.Management.Automation.PSCredential('administrator', $ss)
$cred.getNetworkCredential() | fl
	mb@letmein@SERVER#acc
```