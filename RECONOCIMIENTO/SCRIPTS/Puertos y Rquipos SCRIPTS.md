
**ENUMERADOR DE EQUIPOS**
```sh
for i in $(seq 1 254); do
     timeout 1 bash -c "ping -c 1 192.168.122.$i" &>/dev/null && echo "[+] Host: 192.168.122.$i - ACTIVE" &
done; wait
```

**ENUMERADOR DE PUERTOS**
```sh
for port in $(seq 1 65535); do
     timeout 1 bash -c "echo ' ' > /dev/tcp/192.168.122.228/$port" 2>/dev/null && echo "[+] Port $port - OPEN" &
done; wait
```
