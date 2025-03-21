
### Archivos y Directorios del Sistema

1. **C:\Windows\System32\config\SAM** – Base de datos de cuentas locales (Security Account Manager).
2. **C:\Windows\System32\config\SYSTEM** – Registro del sistema.
3. **C:\Windows\System32\config\SECURITY** – Configuración de seguridad.
4. **C:\Windows\System32\config\SOFTWARE** – Configuración de software instalado.
5. **C:\Windows\System32\config\DEFAULT** – Perfil de usuario predeterminado.
6. **C:\Windows\System32\config\AppEvent.Evt** – Registro de eventos de aplicaciones.
7. **C:\Windows\System32\drivers\etc\hosts** – Archivo de resolución de nombres.
8. **C:\Windows\System32\winlogon.exe** – Proceso de inicio de sesión de Windows.
9. **C:\Windows\System32\mstsc.exe** – Cliente de Escritorio Remoto de Windows.
10. **C:\Windows\System32\services.exe** – Servicio de control de servicios de Windows.

### Archivos de Registro de Eventos

1. **C:\Windows\System32\winevt\Logs\Application.evtx** – Eventos de aplicaciones.
2. **C:\Windows\System32\winevt\Logs\Security.evtx** – Eventos de seguridad (inicios de sesión, cambios de permisos).
3. **C:\Windows\System32\winevt\Logs\System.evtx** – Eventos del sistema (servicios, hardware).
4. **C:\Windows\System32\winevt\Logs\Microsoft-Windows-PowerShell%4Operational.evtx** – Registro de PowerShell.
5. **C:\Windows\System32\winevt\Logs\Setup.evtx** – Eventos de instalación de Windows.

### Archivos y Directorios de Usuarios

1. **C:\Users\[User]\AppData\Local\Microsoft\Windows\History** – Historial de aplicaciones abiertas.
2. **C:\Users\[User]\AppData\Local\Temp** – Directorio de archivos temporales.
3. **C:\Users\[User]\AppData\Roaming\Microsoft\Windows\Start Menu** – Elementos del menú de inicio.
4. **C:\Users\[User]\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt** – Historial de comandos de PowerShell.
5. **C:\Users\[User]\NTUSER.DAT** – Contiene la configuración del usuario y las claves del Registro.
6. **C:\Users\[User]\AppData\Local\Microsoft\Credentials** – Almacén de credenciales de usuario.
7. **C:\Users\[User]\AppData\Roaming\Microsoft\Windows\Recent** – Archivos y carpetas recientes del usuario.
8. **C:\Users\[User]\Documents** – Documentos personales.
9. **C:\Users\[User]\Desktop** – Escritorio del usuario.
10. **C:\Users\[User]\Downloads** – Carpeta de descargas del usuario.

### Archivos de Configuración de Red y Conexiones

1. **C:\Windows\System32\drivers\etc\hosts** – Resolución de nombres.
2. **C:\Windows\System32\drivers\etc\protocol** – Protocolo de red.
3. **C:\Windows\System32\drivers\etc\services** – Servicios de red y sus puertos.
4. **C:\Windows\System32\drivers\etc\networks** – Configuración de redes.
5. **C:\Windows\System32\config\netlogon.log** – Registro de autenticaciones en red.
6. **C:\Windows\System32\config\SecEvent.Evt** – Registros de eventos de seguridad en red.
7. **C:\Windows\System32\config\AppEvent.Evt** – Registro de eventos de aplicaciones en red.

### Directorios Temporales y de Archivos Temporales

1. **C:\Windows\Temp** – Directorio de archivos temporales del sistema.
2. **C:\Users\[User]\AppData\Local\Temp** – Directorio de archivos temporales de usuario.
3. **C:\Windows\Prefetch** – Archivos prefetch (pueden contener evidencias de aplicaciones abiertas).
4. **C:\Windows\Debug\Netlogon.log** – Registro de inicio de sesión en red.
5. **C:\Windows\memory.dmp** – Volcado de memoria generado tras una caída del sistema.

### Archivos y Directorios de Programas y Aplicaciones

1. **C:\Program Files** – Archivos de programas instalados.
2. **C:\Program Files (x86)** – Programas de 32 bits en sistemas de 64 bits.
3. **C:\ProgramData** – Datos compartidos de aplicaciones y programas instalados.
4. **C:\ProgramData\Microsoft\Windows\Start Menu\Programs** – Programas en el menú de inicio para todos los usuarios.
5. **C:\ProgramData\Microsoft\Windows Defender\Scans\History** – Historial de análisis de Windows Defender.
6. *_C:\ProgramData\Microsoft\Windows\WER*_ – Reportes de errores de Windows.
7. **C:\Program Files\Internet Explorer\iexplore.exe** – Ejecutable de Internet Explorer.
8. **C:\Program Files\Windows Defender** – Archivos de Windows Defender.
9. **C:\Windows\System32\spool\PRINTERS** – Documentos de impresión en espera.
10. **C:\inetpub\wwwroot** – Raíz del servidor web IIS (si está instalado).

### Archivos de Configuración de Bases de Datos

1. **C:\Program Files\MySQL\MySQL Server X.X\data** – Directorio de bases de datos MySQL (si está instalado).
2. **C:\ProgramData\MySQL\MySQL Server X.X** – Datos de bases de MySQL.
3. **C:\Program Files\Microsoft SQL Server\MSSQLXX.MSSQLSERVER\MSSQL\Data** – Archivos de base de datos de SQL Server.
4. **C:\Program Files\PostgreSQL\data** – Archivos de datos de PostgreSQL.
5. **C:\ProgramData\MongoDB\log** – Registros de MongoDB.
6. **C:\ProgramData\Redis** – Directorio de almacenamiento de Redis.

### Archivos y Directorios de Configuración de Servicios y Políticas

1. **C:\Windows\System32\GroupPolicy** – Configuración de políticas de grupo.
2. **C:\Windows\SysWOW64\GroupPolicy** – Configuración de políticas de grupo en sistemas de 64 bits.
3. **C:\Windows\System32\GroupPolicy\User\Scripts\Logon** – Scripts de inicio de sesión de usuario.
4. **C:\Windows\System32\GroupPolicy\Machine\Scripts\Startup** – Scripts de inicio de sistema.
5. *_C:\Windows\System32\drivers*_ – Controladores de dispositivos.
6. **C:\Windows\System32\Tasks** – Tareas programadas de Windows.
7. **C:\Windows\System32\Taskmgr.exe** – Administrador de tareas.
8. **C:\Windows\SysWOW64\Taskmgr.exe** – Administrador de tareas en sistemas de 64 bits.
9. **C:\Windows\System32\gpupdate.exe** – Herramienta de actualización de políticas de grupo.

### Archivos de Seguridad y Cifrado

1. **C:\Windows\System32\secpol.msc** – Política de seguridad local.
2. **C:\Windows\System32\rsop.msc** – Resultados de políticas de grupo.
3. **C:\Windows\System32\Encrypting File System (EFS)** – Archivos cifrados (restringido).
4. **C:\Windows\System32\certlm.msc** – Certificados locales de equipo.
5. **C:\Windows\System32\certmgr.msc** – Administrador de certificados.
6. **C:\ProgramData\Microsoft\Crypto\RSA\MachineKeys** – Claves privadas RSA del sistema.
7. **C:\Windows\System32\config\REPAIR** – Copia de seguridad de archivos de configuración críticos.

### Rutas Relacionadas con el Escritorio Remoto y RDP

1. **C:\Windows\System32\mstsc.exe** – Ejecutable de Remote Desktop.
2. **C:\Users\[User]\Documents\Default.rdp** – Configuración predeterminada de RDP.
3. **C:\Windows\System32\termsrv.dll** – Librería de servicio de terminal.
4. **C:\Windows\System32\drivers\tssecsrv.sys** – Controlador de Escritorio Remoto (RDP).
5. **C:\Windows\ServiceProfiles\NetworkService\AppData\Local\Microsoft\Windows\RemoteDesktopClient** – Configuración de clientes de RDP.