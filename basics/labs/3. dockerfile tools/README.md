# Laboratorio Dockerfile Tools

En este laboratorio se genera un Dockerfile más complejo en el que, basándonos en una imagen de Debian, instalaremos herramientas de Linux para realizar pruebas. Al ejecutarse el contenedor, este muestra los resultados de los comandos en pantalla y luego se elimina automáticamente.

---

## Pasos

### Paso 1: Crear el Dockerfile
Crea un nuevo archivo llamado `Dockerfile_tools` en una nueva carpeta y agrega el siguiente contenido:

```dockerfile
# Usa una imagen base Debian
FROM debian:bullseye

# Actualiza e instala las herramientas
RUN apt-get update && apt-get install -y \
    iputils-ping \
    tcpdump \
    dnsutils \
    curl

# Configura tcpdump para mostrar solo algunas líneas
ENV TCPDUMP_OPTIONS -c 5

# Ejecuta comandos al crear el contenedor
CMD echo "Resultado de ping a www.google.com:" && ping -c 3 www.google.com && \
    echo "\nResultado de tcpdump en la interfaz local (mostrando solo algunas líneas):" && tcpdump $TCPDUMP_OPTIONS && \
    echo "\nResultado de dig al dominio cnn.com:" && dig cnn.com && \
    echo "\nResultado de curl a www.google.com:" && curl -I www.google.com
```

### Paso 2: Construir la imagen Docker
1. Abre una terminal y navega hasta la carpeta que contiene el archivo `Dockerfile_tools`.
2. Ejecuta el siguiente comando para construir la imagen Docker:

```bash
docker build -t tu_usuario_docker/nombre_imagen_tools:v1 -f Dockerfile_tools .
```

### Paso 3: Ejecutar el contenedor
Ejecuta el contenedor con el siguiente comando:

```bash
docker run --rm tu_usuario_docker/nombre_imagen_tools:v1
```

Este comando imprimirá en la terminal los resultados de los comandos especificados en el `CMD` del Dockerfile. El contenedor se eliminará automáticamente al finalizar.

---

## Personalizaciones

Puedes ajustar el Dockerfile según tus necesidades:

- **Dominios/IPs:** Puedes pasar variables de entorno para seleccionar el dominio o IP al que se realiza `ping`, `curl`, etc.
- **Comandos adicionales:** Agrega más herramientas o comandos al Dockerfile si deseas realizar pruebas más completas.

Ejemplo de ejecución con variables de entorno:

```bash
docker run --rm -e PING_TARGET=example.com tu_usuario_docker/nombre_imagen_tools:v1
```

Ajusta el `CMD` del Dockerfile para leer y usar las variables de entorno personalizadas.

---

## Nota

Se recomienda crear los archivos desde cero para reforzar el aprendizaje. Si tienes dudas, puedes usar los ejemplos proporcionados como referencia.

