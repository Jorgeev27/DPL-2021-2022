# Tarea 16: Clusterizando una app en Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Desplegando un cluster de Jboss con Docker

Antes de ello, procedemos a instalar Docker Compose. Añadiremos el comando:

    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-composeusr/local/bin/docker-compose

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%201.png)

Cambiamos los permisos:

    sudo chmod +x /usr/local/bin/docker-compose

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%202.png)

Y creamos un enlace simbólico:

    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compos

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%203.png)

Comprobamos la versión instalada:

    docker-compose --version

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%204.png)

 ### 1. DESPLEGANDO UN CLUSTER DE JBOSS CON DOCKER

Cogemos el proyecto de la app de Java, donde hay que realizar los siguientes cambios:

Fichero web.xml y sustituye:

    <display-name>app-web-alumno</display-name>

por:

    <display-name>app-web-aron</display-name>

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%205.png)

donde aron es nuestro nombre.

Fichero index.jsp. Realizar la sustitución del valor alumno siguiendo el mismo patrón que las anteriores tareas.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%206.png)

Lanzamos el comando:

    mvn clean install

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%207.png)

Una vez realizado, encontraremos la carpeta target donde se encuentra app-web-alumno.war, donde se especifica dentro del fichero pom.xml en la etiqueta finalName. Este nombre se especifica dentro del fichero pom.xml.

Una vez construido el proyecto, ejecutamos el resultado en modo local:

    mvn clean jetty:run

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%208.png)

viendo en la salida en el navegador el Hola Mundo!!.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildfly%2010.png)

Construimos el fichero Dockerfile. Hay que construir el fichero Dockerfile, dentro de la carpeta de nuestra aplicación. Dicho fichero, contendrá:

    FROM jboss/wildfly

    ARG WAR_FILE=target/*.war
    ##COPY ${JAR_FILE} app.jar

    ADD ${ARG} /opt/jboss/wildfly/standalone/deployments/

    ARG WILDFLY_NAME
    ARG CLUSTER_PW

    ENV WILDFLY_NAME=${WILDFLY_NAME}
    ENV CLUSTER_PW=${CLUSTER_PW}

    ENTRYPOINT /opt/jboss/wildfly/bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0 -Djboss.server.default.config=standalone-full-ha.xml -Djboss.node.name=${WILDFLY_NAME} -Djava.net.preferIPv4Stack=true -Djgroups.bind_addr=$(hostname -i) -Djboss.messaging.cluster.password=${CLUSTER_PW}

Se está realizando la copia del fichero.war dentro de la carpeta deployments, para posteriormente crear el arranque en cluster. Para continuar hay que realizar el fichero docker-compose.yml para la construcción del cluster.

    version: '3.5'
    services:

    wildfly1:
        build:
        context: .
        args:
          WILDFLY_NAME: wildfly_1
          CLUSTER_PW: secret_password
        image: wildfly_1
        ports:
          - 8080:8080
        networks:
          wildfly_network:

    wildfly2:
        build:
        context: .
        args:
          WILDFLY_NAME: wildfly_2
          CLUSTER_PW: secret_password
        image: wildfly_2
        ports:
          - 8081:8080
        networks:
        wildfly_network:

        networks:
        wildfly_network:
          ipam:
            driver: default

Para crear el cluster de 2 nodos ejecutamos la sentencia:

    sudo docker-compose up

Tras una espera de unos segundos, se tiene desplegada la aplicación en los puertos 8080 y 8081.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2012.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2013.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2014.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2015.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2016%20-%20Clusterizando%20una%20app%20en%20Wildfly/Cluster%20Wildlfy%2016.png)

Me da error 404.
