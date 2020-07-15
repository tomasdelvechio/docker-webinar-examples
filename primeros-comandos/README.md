# Primeros comandos

Se presentan los pirmeros comandos para interactuar con el engine de Docker

## Docker ejecutar contenedores y ver si estan se ejecutaron
## ps, ps -a, stop, run, run -d

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
ahora podemos ver que el contenedor esta corriendo

```bash
docker ps

docker ps -a
```
## Deocker Ingresar al contenedor
## Docker run -it, 

Revisamos que version de SO tenemos
luegos vemos que version tenemos en el contenedor
vemos que estamos usando los comandos dentro del contenedor

```
cat /etc/*release*

docker run -it ubuntu bash 

cat /etc/*release*

```

```bash
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/

docker build -t my-apache2

docker run -dit --name my-running-app -p 8080:80 my-apache
docker run httpd
```





