
### EXTRAER CONTENIDO DEL SYSVOL CREANDO UNIDAD LOGICA AUTENTICANDONOS.
```shell
PS C:\Users\BTables\Documents> net use x: \\dc.fulcrum.local\SYSVOL /user:FULCRUM\BTables ++FileServerLogon12345++
The command completed successfully.
PS C:\Users\BTables\Documents> X:
PS X:\> dir
fulcrum.local
```

### ARCHIVOS CIFRADOS EN WINDOWS.
```shell
PS C:\Users\tolu\Desktop> cipher /c user.txt
```