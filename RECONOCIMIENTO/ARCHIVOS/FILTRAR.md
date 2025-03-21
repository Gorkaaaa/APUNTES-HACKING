

### DOS VALORES USANDO STRINGS
```shell
#DOS TIPOS DE ARCHIVOS Y DOS VALORES
find -type f \( -name "*.log" -o -name "*.txt" \) -exec strings {} + | grep -Ei "user|password"

#UNA PALABRA
find . -type f -exec grep -Hi -E "sql" {} \;

#UNA PALABRA CON DOS LINEAS PARA TENER CONTEXTO
find . -type f -exec grep -Hi -C 2 -E "sql" {} \;

#DOS PALABRAS
find . -type f -exec grep -Hi -E "sql.*error|error.*sql" {} \;
```

### TREE EN LINUX
```shell
#DOS TIPOS DE FORMATO
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'

find . -print | awk '{gsub(/[^\/]*\//, "│   ")}1'
```

### ENCONTRAR UN ARCHIVO ESPECÍFICO
```shell
find . -type f -name "fieldtypederby.xml"
```


### VER DIFERÉNCIAS DE UN DIRECTORIO A OTRO
```shell
❯ diff ./FOLDER ./FOLDER | less
	# LO QUE ESTE CON < ES QUE SE HA QUITADO Y EL > SE HA AGREGADO EN EL SEGUNDO ARCHIVO.
```