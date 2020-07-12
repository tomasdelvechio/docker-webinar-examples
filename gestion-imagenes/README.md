# Gestión de Imagenes

Un conjunto de ejemplos sobre como se manejan imagenes en Docker

## Ejemplo 1

Objetivo: Ejecutar un script php con el CLI del lenguaje sin tenerlo instalado en el Host. Para ello se creara una imagen que ejecute dicho contenedor.

```bash
mkdir -p ~/workspace/webinar-docker/ejemplo-1/
cd ~/workspace/webinar-docker/ejemplo-1/
nano Dockerfile
```

Armar el siguiente Dockerfile
```Dockerfile
FROM php:7-cli
COPY . /tmp/app
WORKDIR /tmp/app
CMD [ "php", "./script.php" ]
```

Luego ejecutar los siguientes comandos

```bash
# Creacion de un script PHP
echo "<?php echo 'Hola Mundo desde PHP';" > script.php
# Generacion de la imagen
docker build --tag webinar/ejemplo-1 .
# Ver imagenes disponibles
docker images
# Buscamos en la ayuda el comando que necesitamos
docker --help
# Buscamos dentro de run, el formato del comando
docker run --help
# Se ejecuta el container a partir de la imagen creada
docker run webinar/ejemplo-1
```

## Ejemplo 2

Objetivo: Mostrar el ciclo de vida efimero de un contenedor.

```bash
# Ejecutar una consola dentro de un contenedor, en base a la distro alpine
docker run -it alpine sh
# Dentro del contenedor
curl www.google.com
# Error, entonces instalar curl
apk add curl
# Una vez que instala, ejecutar nuevamente curl
curl www.google.com
# exito! salir del contenedor
exit
```

En este punto se genero un container, se instalo curl, y se recupero un sitio. ¿Que sucede si se intenta realizar el experimento nuevamente?

```bash
docker run -it alpine sh
curl www.google.com
exit
# Revisar los contenedores
docker ps -a | head -n 3
```
