# Tarea 12: Instalación de PHP para Apache y Nginx en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalar Docker
 - Trabajar con imágenes de Docker
 - Administrar contenedores de Docker

Posiblemente, no se tenga la versión más reciente de Docker hasta la fecha. Para ello, actualizaremos Docker desde el repositorio oficial de éste. Agregaremos nuevas fuentes de paquetes y la clave GPG de Docker para garantizar que las descargas sean válidas, y después instalaremos el paquete.

 ### 1. INSTALAR DOCKER

Primeramente, actualizamos la lista de paquetes. Para ello, utilizaremos el comando:

    sudo apt update

A continuación, instalamos los paquetes de los requisitos previos que permiten a apt usar los paquetes a través de HTTPS. Para ello, utilizaremos el comando:

    sudo apt install apt-transport-https ca-certificates curl software-properties-common

Y añadimos la clave de GPG para el repositorio oficial de Docker en su sistema. Para ello, utilizaremos el comando:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Y agregamos el repositorio de Docker a las fuentes de APT:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

Después de ello, actualizamos el paquete de base de datos con los paquetes de Docker del repositorio recién agregado:

    sudo apt update

Hay que asegurarse que estamos haciendo los pasos correctamente para realizar la instalación desde el repositorio de Docker en el lugar del repositorio predeterminado de Ubuntu:

    apt-cache policy docker-ce

Y se verá el número de la versión de Docker distinto:

    Installed: (none)
    Candidate: 5:19.03.9~3-0~ubuntu-focal
    Version table:
         5:19.03.9~3-0~ubuntu-focal 500
         500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages

Para finalizar, instalamos Docker con el comando:

    sudo apt install docker-ce

Con Docker instalado, el dominio de éste se iniciará y el proceso se habilitará para ejecutarse en el inicio. Para ver si funciona, ejecutamos el comando:

    sudo systemctl status docker

Y el resultado es el siguiente:

    docker.service - Docker Application Container Engine
         Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset>
         Active: active (running) since Fri 2021-10-29 19:21:13 WEST; 28min ago
    TriggeredBy: ● docker.socket
           Docs: https://docs.docker.com
       Main PID: 3169 (dockerd)
          Tasks: 10
         Memory: 38.3M
         CGroup: /system.slice/docker.service
                 └─3169 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/cont>


  ### 2. TRABAJAR CON IMÁGENES DE DOCKER

Para verificar si se puede acceder a las imágenes y descargarlas de Docker Hub, escribimos el comando:

    docker run hello-world

Y el resultado será el siguiente:

    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
    3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

Aquí en este punto me surgió un problema y es que no podía crearlo porque no tenía los permisos. Lo solventé dándole permisos, con el comando:

    sudo chmod 666 /var/run/docker.sock

De este comando no le saqué captura porque se me olvidó pero está realizado.

  ### 2. ADMINISTRAR CONTENEDORES DE DOCKER

Después de usar Docker por un tiempo, habrá muchos contenedores en ejecución e inactivos. Para visualizar los activos, utilizaremos el comando:

    sudo docker ps

Y el resultado es el siguiente:

    CONTAINER ID        IMAGE               COMMAND             CREATED

Para ver todos los contenedores activos e inactivos, utilizaremos el comando:

    sudo docker ps -a

Y resultado es el siguiente:

    CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
    b2c5683bc38f   hello-world   "/hello"   14 minutes ago   Exited (0) 14 minutes ago             kind_curran

Para ver el último contenedor creado, utilizaremos el comando:

    sudo docker ps -l

Y el resultado es el siguiente:

    CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
    b2c5683bc38f   hello-world   "/hello"   24 minutes ago   Exited (0) 23 minutes ago             kind_curran

Si queremos listar las imágenes de Docker de nuevo, se nos mostrará la nueva imagen, así como la anterior que derivamos. Para ello, utilizaremos el comando:

    sudo docker images

Y el resultado es el siguiente:

    REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
    hello-world   latest    feb5d9fea6a5   5 weeks ago   13.3kB
