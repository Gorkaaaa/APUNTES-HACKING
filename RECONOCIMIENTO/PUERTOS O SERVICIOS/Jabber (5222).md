
# INSTALAR PIDGIN
```shell
sudo apt install pidgin
```

# CONFIGURACIÓN 
1. Protocolo: XMPP
2. En caso de no tener credenciales agregar la opción de agregar nueva cuenta al servidor.
3. Avanzada > Conectar al servidor: IP DEL SERVIDOR
4. FINALIZAR LA CREACIÓN DE LA CUENTA
5. Menu de arriba > Cuentas > SELECCIONAMOS LA CUENTA > Habilitar cuenta.

# ACCEDER A UNA SALA
1. (CON LA CUENTA CREADA)
2. Herramientas > Lista de Salas > (SI NO SALE NINGUNA) Obtener lista de salas.

# ENUMERAR USUARIOS
### MÉTODO 1
1. MENU DE ARRIBA > Cuentas > Mi cuenta > Buscar ususarios

### MÉTODO 2
```shell
#EJECUTAR ESTE COMANDO Y REALIZAR EL METODO 1
pidgin --debug | tee results.txt

#EXPORTAR CONTENIDO DE results.txt
cat results.txt | grep -oP '(?<=<value>).*?(?=</value>)' | grep "jab.htb" | sort -u #CON ESTO TENDRIAMOS TODOS LOS USUARIOS CON EL CORREO

cat results.txt | grep -oP '(?<=<value>).*?(?=</value>)' | grep "jab.htb" | sort -u | awk '{print $1}' FS="@" #CON ESTO TENDRIAMOS TODOS LOS USUARIOS SIN EL CORREO RECOMENDABLE PARA ASREPROAST
```
