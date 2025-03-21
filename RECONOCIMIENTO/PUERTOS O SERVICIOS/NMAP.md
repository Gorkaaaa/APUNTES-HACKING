
## TCP
```shell
#SERVICIO
sudo nmap -p- -Pn -n -vvv -sS --min-rate 500 192.168.226.130 -oG target.txt

#VERSION
nmap -p21,22,25,53,80,110,143,465,587,993,995,2525,3306,8080,8083,8443 -A -sCV 192.168.219.156 -oN allPorts

#AMBAS
sudo nmap -p- -Pn -n -vvv -sS -sCV --min-rate 500 192.168.226.130 -oG target.txt


nc -zv 192.168.0.1 1-65535 2>&1 | grep -v refused
```

## UDP
```bash
sudo nmap 10.10.11.40 -sU -Pn -vvv --top-ports 150

sudo nmap 192.168.219.156 -p161,69 -sU -Pn -vvv

nc -zv 192.168.0.1 1-65535 2>&1 | grep -v refused
```


# IPv6

## ENUMERACIÓN GENERAL
```shell
❯ sudo nmap -p- --min-rate 5000 -sS -T5 -Pn -n -6 dead:beef::57a:71c:23:77a
```

**ENUMERACIÓN ESPECIFICA POR NMAP**
```shell
❯ sudo nmap -p8730 -sCV -6 dead:beef::57a:71c:23:77a
```


# SCRIPTS

## WEB
```shell
nmap --script http-enum -p80 target.site -oN WebScanTarged
```

## LDAP
```shell
❯ nmap -n -sV --script "ldap* and not brute" -Pn 10.10.10.182
```

### IDENTIFICAR SI ES VULNERABLE
```SHELL
❯ nmap --script "smb-vuln-ms17-010" -p445 10.10.10.74

❯ nmap --script "smb-vuln-ms17-010" -p445 10.10.10.40

❯ nmap --script "vuln and safe" -p445 10.10.10.40
```