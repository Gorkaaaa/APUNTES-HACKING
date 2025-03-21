
# EN MÁQUINA VICTIMA LINUX
```shell
www-data@apocalyst:/var/www/html/apocalyst.htb$  script -c bash /dev/null
www-data@apocalyst:/var/www/html/apocalyst.htb$ ^Zzsh: suspended
❯ stty raw -echo; fg
	reset xterm
www-data@apocalyst:/var/www/html/apocalyst.htb$ export TERM=xterm
www-data@apocalyst:/var/www/html/apocalyst.htb$ export SHELL=/bin/bash

❯ stty size
44 184

www-data@apocalyst:/var/www/html/apocalyst.htb$ stty rows 44 columns 184
```


### POSIBLE PROBLEMA CON EL NANO
```shell
[dentro de la máquina victima.]
stty -ixon
```


### TRATAMIENTO DE LA TTY CON PYTHON
```shell
python3 -c "import pty;pty.spawn('/bin/bash')"
```


### EXTRA
```bash
script /dev/null -c bash
python -c 'import pty; pty.spawn("/bin/bash")'
python2 -c 'import pty; pty.spawn("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'
stty raw -echo;fg
reset xterm-color
export TERM=xterm
stty rows 46 columns 184
```