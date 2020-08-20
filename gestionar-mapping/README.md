## Ejemplos de Tags - Mapeo de puertos - Mapeo de directorios 

# Mapeo De Puertos

se muestra como se mapeo el puerto 5050 sel dost al puerto 8080 del contenedor

```bash

docker run -p 5050:8080 kodekloud/simple-webapp


```

dirigirse a http://localhost:8081/

se pueden correr varios sin problema

```bash

docker run -p 5050:8080  -d kodekloud/simple-webapp

docker run -p 5051:8080 -d kodekloud/simple-webapp

docker run -p 5052:8080 -d kodekloud/simple-webapp

docker ps


```

podemos ver algo como esto, donde estan los contenedores corriendo con el mapeo de los puertos

```bash
CONTAINER ID    IMAGE                       COMMAND             PORTS                       NAMES
6516cc6a267a    kodekloud/simple-webapp     "python app.py"     0.0.0.0:5050->8080/tcp      cool_feynman
47d8534db6fa    kodekloud/simple-webapp     "python app.py"     0.0.0.0:5051->8080/tcp      pedantic_zhukovsky
2800dda57efd    kodekloud/simple-webapp     "python app.py"     0.0.0.0:5052->8080/tcp      competent_diffie

```

y nos podemos dirigir a 

dirigirse a http://localhost:5050/
dirigirse a http://localhost:5051/
dirigirse a http://localhost:5052/

# Mapeo De Directorios

Vamos a probar una base de datos donde necesitamos almacenar las bases de datos

```bash

#descargo la imagen
docker pull ubuntu
#corro el contenedor de forma interactiva para tener acceso a la linea de comandos
docker run -it ubuntu bash
# creao un archivo en el home 

echo "'Hola Mundo desde " > /home/hola_mundo.txt
# salgo del contenedor
exit
#vuelvo a correr el contendor e intento abir el archivo
docker run -it ubuntu bash
cat /home/hola_mundo.txt
#no esxiste el archivo

# vuelvo a repetir lo anterior, pero en esta oportunidad mepo a un volumen en el host
docker run -v scripts:/tmp/app/ -it webinar/ejemplo-1 bash 
# creo el documento salgo del contenedor y vuelvo a abrir el archivo
echo "'Hola Mundo desde " > /home/hola_mundo.txt
exit
docker run -v scripts:/tmp/app/ -it webinar/ejemplo-1 bash 
cat /home/hola_mundo.txt

```
