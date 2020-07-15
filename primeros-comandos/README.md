#Primeros comandos

Se presentan los pirmeros comandos para interactuar con el engine de Docker

##

docker run, ejecuta una imagen y si no la encuentra localmente la descarga del registry configurada

```bash
docker run hello-world
```

Listar los contenedores que estan corriendo
Se van a ver los contenedores que estan corriendo con la siguiente informacion

CONTAINER ID - IMAGE - COMMAND - CREATED - STATUS - PORTS


```bash
docker ps
```

No se ve el contenedor hello-world, porque ya termino su ejecucion

```bash
docker ps -a
```
Ahora podemos ver los contenedor que se estan ejecutando y se ejecutaron


```bash
docker run kodekloud/simple-webapp
```
De esta forma podemos ver que el contenedor queda corriendo pero no nos devuelve el prompt
agregando -d queda corriendo en segundo plano
CTRL+C para salir

```bash
docker run -d kodekloud/simple-webapp
```
```bash
docker ps
```

```bash
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/

docker build -t my-apache2

docker run -dit --name my-running-app -p 8080:80 my-apache
docker run httpd
```





