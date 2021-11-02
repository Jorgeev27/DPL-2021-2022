# Tarea 14: Instalación de Wildfly en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Descarga de la imagen del docker Wildfly

 ### 1. DESCARGA DE LA IMAGEN DEL DOCKER WILDFLY

Este paso es opcional porque al construir la imagen basada en el fichero Dockerfile se descargará la imagen base si no la tenemos en nuestro repositorio. Vamos a descargar la versión 25.0.0.Final de la imagen oficial. Para ello, utilizaremos a utilizar el tag correspondiente

    sudo docker pull jboss/wildfly:25.0.0.Final

Y el resultado es el siguiente:

    25.0.0.Final: Pulling from jboss/wildfly
    f87ff222252e: Pull complete
    13776e8da872: Pull complete
    0b43aea4eeb1: Pull complete
    8116b2f7ca5a: Pull complete
    f26d32e28c29: Pull complete
    Digest: sha256:35320abafdec6d360559b411aff466514d5741c3c527221445f48246350fdfe5
    Status: Downloaded newer image for jboss/wildfly:25.0.0.Final
    docker.io/jboss/wildfly:25.0.0.Final

Ahora toca ver el listado de las imágenes descargadas con el comando:

    sudo docker images

Y el resultado es el siguiente:

    REPOSITORY      TAG            IMAGE ID       CREATED       SIZE
    jboss/wildfly   25.0.0.Final   856694040847   3 weeks ago   736MB
    hello-world     latest         feb5d9fea6a5   5 weeks ago   13.3kB

Ahora, arrancamos un contenedor con esa imagen y comprobamos qué tenemos disponible en el servidor de aplicaciones. Para ello, utilizaremos el comando:

    sudo docker run -d -p 5000:8080 --name "servidor-desa" jboss/wildfly

Y el resultado es:

    Unable to find image 'jboss/wildfly:latest' locally
    latest: Pulling from jboss/wildfly
    Digest: sha256:35320abafdec6d360559b411aff466514d5741c3c527221445f48246350fdfe5
    Status: Downloaded newer image for jboss/wildfly:latest
    c1bdc66aa180bda8936fb538b95faf8d18f3aec2aa97ca5da0bcd5e5f87412b6

Y realizando el comando:

    ip a

Para comprobar la dirección IP 172.17.0.1:

    3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
      link/ether 02:42:1e:e0:9b:4a brd ff:ff:ff:ff:ff:ff
        inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
         valid_lft forever preferred_lft forever
      inet6 fe80::42:1eff:fee0:9b4a/64 scope link
         valid_lft forever preferred_lft forever

De este modo, si se accede a 172.17.0.1:5000 veremos la instalación de Wildfly.
