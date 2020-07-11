# Gestión de Imagenes

Un conjunto de ejemplos sobre como se manejan imagenes en Docker

## Ejemplo 1

Ejecutar un script php con el CLI del lenguaje sin tenerlo instalado en el Host.

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
