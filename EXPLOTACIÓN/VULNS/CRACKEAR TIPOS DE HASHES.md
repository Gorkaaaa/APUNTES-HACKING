
```shell
hashcat --help | grep Kerberos #GREPEAMOS POR EL QUE NECESITEMOS.
hashcat -m 13100 hash -o pass.txt /usr/share/wordlists/rockyou.txt --force #DESPUÉS DEL -m INDICAMOS EL TIPO DE HASH
```

```shell
hashcat -m 1000 hashes /usr/share/wordlists/rockyou.txt
```