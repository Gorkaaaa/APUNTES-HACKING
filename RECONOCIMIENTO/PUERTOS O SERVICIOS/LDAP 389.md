
### ENUMERACIÓN VISUAL
```shell
❯ ldapdomaindump -u 'search.htb\hope.sharp' -p 'IsolationIsKey?' 10.10.11.129

❯ sudo php -S 0.0.0.0:80
go to localhost / FILE in the folder.
```

### ENUMERACIÓN BÁSICA
```shell
ldapsearch -x -H ldap://10.10.10.172 -s base namingcontexts

ldapsearch -x -H ldap://10.10.11.41 -b "DC=certified,DC=htb"
```

### LDAPSearch
```bash
ldapsearch -x -H ldap://10.10.11.174 -D 'support\ldap' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "CN=Users,DC=support,DC=htb"

ldapsearch -x -H ldap://10.10.11.174 -D '' -w '' -b "CN=Users,DC=support,DC=htb"

ldapsearch -x -H ldap://10.10.11.174 -D 'ldap@support.htb' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b 'DC=support,DC=htb' | grep -i "samaccountname: support" -B 50
```


### NMAP
```shell
❯ nmap -n -sV --script "ldap* and not brute" -Pn 10.10.10.182

---------------------------
git clone https://github.com/ropnop/windapsearch.git
pip install python-ldap
./windapsearch.py -U --full --dc-ip 10.10.10.182
```