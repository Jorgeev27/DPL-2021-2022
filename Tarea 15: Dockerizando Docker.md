# Tarea 15: Dockerizando Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Creación del fichero dockerfile para Wildfly
 - Uso de la nueva imagen

 ### 1. CREACIÓN DEL FICHERO DOCKERFILE PARA WILDFLY

Creamos el fichero de trabajo en cualquier parte del sistema. En este caso, la creamos en la raíz con el comando:

    mkdir wildfly-config

Y accedemos a la carpeta:

    cd wildfly-config/

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%201.png)

Creamos dentro de la carpeta el fichero de configuración con el siguiente comando:

    sudo nano dockerfile

Y añadimos la siguiente configuración de nuestra imagen:

    # Base image
    FROM jboss/wildfly:25.0.0.Final

    # Maintainer
    MAINTAINER "jpexposito" "mail@example.com"

    # Create user admin with password admin
    RUN /opt/jboss/wildfly/bin/add-user.sh admin admin --silent

    # Add custom configuration file
    # ADD standalone.xml /opt/jboss/wildfly/standalone/configuration/

    # Add example.war to deployments
    # ADD example.war /opt/jboss/wildfly/standalone/deployments/

    # JBoss ports
    EXPOSE 8080 9990 8009

    # Run
    CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone.xml"]

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%202.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%203.png)

Ahora, construimos la imagen:

    sudo docker build -q --rm --tag=jboss/wildfly:25.0.0.Final-config .

Y nos muestra la siguiente salida que indica que se ha construido correctamente:

    sha256:56d2170193f556698a65abda6722ba29e877ee52b5df6b35ff3f1048d74ee381

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%204png)

Después, se verifica si existe la imagen dentro de docker. Para ello, utilizamos el comando:

    sudo docker images

Con la siguiente salida:

    REPOSITORY      TAG                    IMAGE ID       CREATED        SIZE
    jboss/wildfly   25.0.0.Final-config    56d2170193f5   12 hours ago   736MB

Y voila, primera imagen en Docker!!.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%205png)

  ### 2. USO DE LA NUEVA IMAGEN

Vamos a probar la imagen de docker creada recientemente. Para ello, utilizamos el comando:

    sudo docker run -d -p 8080:8080 -p 9990:9990 -p 8009:8009 --name servidor-wilfly-config -it jboss/wildfly:25.0.0.Final-config

Teniendo en cuenta que el parámetro --name servidor-wildfly-config que indica el nombre del servidor que hemos creado y arrancado, y que deber ser significativo. Y obtendremos algo similar a lo siguiente:

    f02cdd6962b18134ba34e6ba03331a65526c30fdcf3d961ac8d4817b7f0007e5

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%206png)

Una vez realizado la acción, se debe de ejecutar la sentencia que verifica que el contenedor está arrancado:

    sudo docker ps -a

Y accedemos a la consola de Wildfly, para verificar que se puede entrar a la consola de administración con el usuario admin.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%207png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%208png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%209png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2015%20-%20Dockerizar%20Wildfly/Dockerizar%20Wildfly%2010png)
