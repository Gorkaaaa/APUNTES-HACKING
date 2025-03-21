
### ENUMERACIÓN
```shell
❯ curl -s -X GET 'http://10.10.11.161/api' | jq
```


### POST
```shell
#LA TRAMITA POR JSON
❯ curl -s -X POST 'http://10.10.11.161/api/v1/user/signup' -H "Content-Type: application/json" -d '{"username":"Gorka", "password":"Gorka123"}' | jq

#LA TRAMITA CON &
❯ curl -s -X POST "http://10.10.11.161/api/v1/user/login" -d 'username=test1@backend.htb&password=test1' | jq
```


### CON HEADERS
```shell
❯ curl -s -X GET 'http://10.10.11.161/api/v1/admin/' -H "Authorization: Bearer eyJhbG....token..." | jq
```