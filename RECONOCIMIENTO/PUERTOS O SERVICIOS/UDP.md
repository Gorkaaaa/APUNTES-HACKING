
---
**ESCANEO POR UDP**

---
**NMAP**
```r
❯ nmap -sU --top-ports 100 --open -n 10.10.10.241 -oG UDP
PORT    STATE SERVICE
161/udp open  snmp
```