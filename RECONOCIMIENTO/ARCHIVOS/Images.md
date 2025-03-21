
### METADATOS
```shell
❯ exiftool img.img
```

### STRINGS DE LA FOTO
```shell
#TODO EL CONTENIDO DE LA FOTO
strings img.img

#LISTAR TODAS LAS LINEAS QUE TIENE LA FOTO
strings img.img | wc -l

#LISTAR TODO EL CONTENIDO IGUAL O MAYOR A 10 CARACTERES.
strings img.img | head -n 10
```

### STEGANOGRAFÍA
```shell
#VER SI HAY CONTENIDO EN LA FOTO
❯ steghide info img.img

#EXTRAER CONTENIDO DE LA FOTO
❯ steghide extract -sf image.jpg
```