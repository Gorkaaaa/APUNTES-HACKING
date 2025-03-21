

---
**ENUMRACIÓN**

---
**COMMUNITY STRING**
```r
❯ onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt 10.10.10.241
10.10.10.241 [public] Linux pit.htb 4.18.0-305.10.2.el8_4.x86_64 #1 SMP Tue Jul 20 17:25:16 UTC 2021 x86_64
```

**INSTALACIÓN**
```r
❯ apt install snmp-mibs-downloader
...
```

**CAMBIAR CONTENIDO DE ARCHIVO DE CONFIGURACIÓN**
```r
❯ vi /etc/snmp/snmp.conf

4   │ mibs :

-------------------

4   │ #mibs :
```

**LISTAR INFORMACIÓN DE UN USUARIO Y UN PROCESO**
```r
❯ snmpwalk -v2c -c public 10.10.10.241 1
snmpwalk -c public -v1 192.168.128.145 1.3.6.1.2.1.25.6.3.1.2

❯ snmpwalk -v 1 -c public 10.10.11.136


snmpwalk -v2c -c public 192.168.248.149 NET-SNMP-EXTEND-MIB::nsExtendObjects

snmpwalk -v 2c -c public 192.168.248.149 NET-SNMP-EXTEND-MIB::nsExtendOutputFull

```

---
**RCE**

---
**snmpwalk**
```r
❯ snmpwalk -v2c -c public  10.10.10.241 1

[*AQUI PODEMOS ENUMERAR DOS USUARIOS*]
Login Name           SELinux User         MLS/MCS Range        Service

__default__          unconfined_u         s0-s0:c0.c1023       *
michelle             user_u               s0                   *
root                 unconfined_u         s0-s0:c0.c1023       *

[*PODEMOS VER UN BINARIO QUE SE ESTÁ EJECUTANDO*]
NET-SNMP-EXTEND-MIB::nsExtendCommand."monitoring" = STRING: /usr/bin/monitor
```

**LISTAR INFORMACIÓN EXTRA**
```r
❯ snmpbulkwalk -v2c -c public  10.10.10.241 1
UCD-SNMP-MIB::dskPath.2 = STRING: /var/www/html/seeddms51x/seeddms
```