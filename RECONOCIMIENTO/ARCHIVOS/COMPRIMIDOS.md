
### LISTAR CONTENIDO DE UN COMPRIMIDO
```shell
❯ 7z l app_backup_1635803546.zip
```

### DESCOMPRIMIR UN ARCHIVO
```shell
❯ unzip app_backup_1635803546.zip
```

### TAR
```shell
tar -xvf 939348555.tar
```

# ZIP2JOHN
```shell
zip2john winrm_backup.zip > zip.john 
john zip.john -wordlist:/usr/share/wordlists/rockyou.txt
```