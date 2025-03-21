# REG.py
```SHELL
#SI NO FUNCIONA HKCR podemos probar con HKCU, HKLM, HKU, HKCC, HKPD
reg.py htb.local/henry.vinson@apt -hashes :HASH(SI NO ES HASH PUES CONTRASEÑA) query -keyName 'HKCR' 



#UNA VEZ HEMOS ENCONTRASO UNO PARA ACCEDER...
reg.py htb.local/henry.vinson@apt -hashes :HASH(SI NO ES HASH PUES CONTRASEÑA) query -keyName 'HKCR\nombre del que queramos' 
```