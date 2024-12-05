
# Ejercicio: Crear y ejecutar un contenedor Docker con Apache

## Paso 1: Crear el directorio de trabajo
Crea un nuevo directorio para este proyecto:

```bash
mkdir apache-docker && cd apache-docker
```

---

## Paso 2: Crear el archivo `index.html`

Dentro del directorio, crea el archivo `index.html` con el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página Básica de Ejemplo</title>
</head>
<body>
    <h1>Hola desde Docker y Apache</h1>
    <p>Esta es una página HTML básica servida por un contenedor de Docker con Apache.</p>
</body>
</html>
```

---

## Paso 3: Crear el archivo `Dockerfile`

En el mismo directorio, crea un archivo llamado `Dockerfile` con el siguiente contenido:

```Dockerfile
# Utiliza la imagen oficial de Apache como base
FROM httpd:2.4

# Copia el archivo index.html al directorio de documentos del servidor Apache
COPY index.html /usr/local/apache2/htdocs/
```

---

## Paso 4: Construir la imagen de Docker

Construye la imagen utilizando el comando:

```bash
docker build -t mi-apache-basico .
```

---

## Paso 5: Ejecutar el contenedor

Ejecuta un contenedor basado en la imagen que acabas de construir. Mapearás el puerto 8080 de tu máquina al puerto 80 del contenedor:

```bash
docker run -d -p 8080:80 mi-apache-basico
```

---

## Paso 6: Probar el servidor

Abre tu navegador web y accede a la dirección:  
[http://localhost:8080](http://localhost:8080)

Deberías ver la página HTML que creaste.

---

## Notas adicionales
- Si necesitas detener el contenedor:  
  ```bash
  docker stop <ID_del_contenedor>
  ```
- Si deseas listar los contenedores en ejecución:  
  ```bash
  docker ps
  ```
- Recuerda que puedes personalizar el contenido del archivo `index.html` según tus necesidades.

---

¡Y listo! Ahora tienes un servidor Apache funcionando dentro de un contenedor Docker. 🎉
