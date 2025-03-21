
### HEX CRYPT PASSWORD
```shell
STRING WITH PASS:"Password"=hex:6b,cf,2a,4b,6e,5a,ca,0f
https://github.com/frizb/PasswordDecrypts  --> This steps follow frizb reposotory

msfconsole
msf5 > irb
key="\x17\x52\x6b\x06\x23\x4e\x58\x07"
require 'rex/proto/rfb'
Rex::Proto::RFB::Cipher.decrypt ["6BCF2A4B6E5ACA0F"].pack('H*'), key
--> "sT333ve2"
```