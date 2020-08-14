# Docker Compose

Acá se encontraran ejemplos desarrollados para Docker Compose

## Ejemplo 1 - Entorno LAMP

Algunas decisiones deben ser tomadas para construir el entorno. ¿Versión de PHP a utilizar? ¿Versión de MySQL? Versión de Apache es mas fácil, la mas nueva, pero cualquiera en la rama 2.4 es perfectamente factible.

Se crea un directorio donde se gestionara nuestro proyecto.

```bash
mkdir -p ~/workspace/webinar-docker/docker-compose/ejemplo-1
cd ~/workspace/webinar-docker/docker-compose/ejemplo-1
echo "<?php phpinfo();" > index.php
touch docker-compose.yml
```

El ultimo archivo generado, `docker-compose.yml`, es el que contiene todo lo que necesitamos para levantar el entorno. En el debemos incluir todo lo que requiera nuestro proyecto para ser ejecutado.

En el caso del ejemplo incluir el siguiente contenido:

```yaml
version: '3'

services:
    web:
        image: php:7.4.9-apache
        ports:
            - 8888:80
        volumes:
            - .:/var/www/html
        links:
            - 'db'
    db:
        image: mysql:8.0
        volumes:
            - mysql_volume:/var/lib/mysql
        environment:
            TZ: "Argentina/Buenos_Aires"
            MYSQL_ALLOW_EMPTY_PASSWORD: "no"
            MYSQL_ROOT_PASSWORD: "webinar-root-pass"
            MYSQL_USER: 'webinar-user'
            MYSQL_PASSWORD: 'webinar-pass'
            MYSQL_DATABASE: 'webinar-db'

    adminer:
        image: adminer
        ports:
          - 8889:8080

volumes:
    mysql_volume:
```

Se puede probar el despliegue con el siguiente comando

```bash
docker-compose up
```

A continuación, ingresando a http://localhost:8888 se puede ver la ejecución de PHP. También se puede ver en http://localhost:8889 la interfaz de Adminer, para realizar tareas administrativas sobre MySQL.

## Ejemplo 2 - Agregando PDO al contenedor de PHP

Asi como esta el ejemplo 1, no es posible conectarse al contenedor de Mysql desde el de PHP usando PDO (porque no viene instalado).

Copiamos el contenido del ejemplo 1 para tomarlo de base:

```bash
cp -r ~/workspace/webinar-docker/docker-compose/ejemplo-1 ~/workspace/webinar-docker/docker-compose/ejemplo-2
cd ~/workspace/webinar-docker/docker-compose/ejemplo-2
```

Alli dentro, crearemos un Dockerfile para nuestro nuevo contenedor de PHP (basado en el utilizado en el ejemplo 1), pero agregando el soporte para PDO y PDO MySQL.

Crearemos entonces un archivo `Dockerfile` y escribiremos el siguiente contenido.

```dockerfile
FROM php:7.4.9-apache
RUN docker-php-ext-install pdo pdo_mysql
```

A continuación es necesario modificar el contenido del service `web`  dentro del archivo `docker-compose.yml`, dejándolo de la siguiente manera

```yaml
    web:
        build: .
        ports:
            - 8888:80
        volumes:
            - .:/var/www/html
        links:
            - 'db'
```

Una vez hecho esto, resta ejecutar solo 2 comandos

```bash
docker-compose build # build de todos los servicios que lo requieran
docker-compose up # inicia el entorno con las imagenes mas actualizadas disponibles
```

