

### FORMULARIO PARA SUBIR ARCHIVOS HTML CON NOMBRE (PARA INTERCEPTAR)
```HTML
<form action="https://tuservidor.com/subir-archivo" method="POST" enctype="multipart/form-data">
        <!-- Campo para seleccionar el archivo -->
    <label for="archivo">Selecciona un archivo:</label>
    <input type="file" id="archivo" name="archivo" required>

        <!-- Campo opcional de nombre -->
    <label for="nombre">Nombre del archivo (opcional):</label>
    <input type="text" id="nombre" name="nombre">

    <!-- Botón para enviar el formulario -->
    <input type="submit" value="Subir Archivo">
</form>
```

### FORMULARIO PARA SUBIR ARCHIVOS HTML SIN NOMBRE (PARA INTERCEPTAR)
```HTML
<form action="https://tuservidor.com/subir-archivo" method="POST" enctype="multipart/form-data">
        <!-- Campo para seleccionar el archivo -->
    <label for="archivo">Selecciona un archivo:</label>
    <input type="file" id="archivo" name="archivo" required>
</form>
```