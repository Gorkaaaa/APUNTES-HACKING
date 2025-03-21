
### AWS LAMBDA
```shell
#ELIMINAR CONFIGURACIÓN
rm ~/.aws/credentials
rm ~/.aws/config

#CONFIGURACIÓN
❯ aws configure

#LISTAR FUNCIONES
❯ aws --endpoint-url=http://cloud.epsilon.htb lambda list-functions

#CONTENIDO DE UNA FUNCIÓN
❯ aws --endpoint-url=http://cloud.epsilon.htb lambda get-function --function-name=costume_shop_v1 | jq .Code.Location
```