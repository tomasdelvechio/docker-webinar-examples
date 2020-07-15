# Primeros comandos

Se presentan los pirmeros comandos para interactuar con el engine de Docker

## Docker ejecutar contenedores y ver si estan se ejecutaron
## ps, ps -a, run, run -d

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
## run -it, 

Revisamos que version de SO tenemos
luegos vemos que version tenemos en el contenedor
vemos que estamos usando los comandos dentro del contenedor

```
cat /etc/*release*

docker run -it ubuntu bash 

cat /etc/*release*

```

## Deocker detener contenedor
## stop


```

docker run  ubuntu
# no se ve el contenedor porque termino

docker ps

#corren en background y se mantiene 30 segundos
docker run -d  ubuntu sleep 30

#podemos ver el conenedor activo, y con el comando sleep 30

docker ps

```

ahora si queremos detener el contenedor antes que termine

```


#corren en background y se mantiene 3000 segundos
docker run -d  ubuntu sleep 3000

#podemos ver el conenedor activo, y con el comando sleep 3000

docker ps

#lo detenemos con el nombre del contenedor  o el id

docker stop nombre_del_contenedor_o_id


```

## Deocker destruir contenedor
## rm

```

docker run -d  ubuntu sleep 3000

docker ps

docker rm nombre_contenedor_o_id

#no se puede porque esta corriendo

docker stop nombre_contenedor_o_id

docker rm nombre_contenedor_o_id

```

## Deocker listar y remover imagenes
## images, rmi

```

docker run -d  ubuntu sleep 3000

docker images


docker rmi ubuntu

#no se puede porque esta corriendo

docker ps

docker stop nombre_contenedor_o_id

# no se puede, tiene contenedores asociados

docker rmi ubuntu

docker ps

docker rm nombre_contenedor_o_id

docker rmi ubuntu
```

## Docker descargar imagen
## pull 
## https://hub.docker.com/


```bash

docker images

docker pull php:7-cli

docker images

```

## Deocker leer contenedores
## logs

```bash

docker logs --help 

docker ps

docker logs nombre_del_contenedor

```


