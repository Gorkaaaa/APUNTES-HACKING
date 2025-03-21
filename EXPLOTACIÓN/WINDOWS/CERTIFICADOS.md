
# HASH
### PFX2JOHN
```shell
❯ pfx2john staff.pfx > hash
❯ pfx2john search-RESEARCH-CA.p12  > hash2

❯ john hash --wordlist=/usr/share/wordlists/rockyou.txt
	--> misspissy

❯ john hash2 --wordlist=/usr/share/wordlists/rockyou.txt
	--> misspissy

#TIP: Si la web no lo reconoce cambia a https ;)
```