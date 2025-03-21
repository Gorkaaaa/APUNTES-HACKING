

### MANDAR QUERY
```shell
curl -s -G http://10.10.10.121:3000/graphql --data-urlencode "query={user}" | jq
```

### ENUMERAR VALOR
```shell
❯ curl -s -G http://help.htb:3000/graphql --data-urlencode 'query={user {username} }' | jq
```