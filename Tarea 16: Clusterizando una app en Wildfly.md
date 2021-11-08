# Tarea 16: Clusterizando una app en Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Desplegando un cluster de Jboss con Docker

 ### 1. DESPLEGANDO UN CLUSTER DE JBOSS CON DOCKER

Cogemos el proyecto de la app de Java, donde hay que realizar los siguientes cambios:

Fichero web.xml y sustituye:

    <display-name>app-web-alumno</display-name>

por:

    <display-name>app-web-aron</display-name>

donde aron es nuestro nombre.

Fichero index.jsp. Realizar la sustitución del valor alumno siguiendo el mismo patrón que las anteriores tareas.

Lanzamos el comando:

    mvn clean install

Una vez realizado, encontraremos la carpeta target donde se encuentra app-web-alumno.war, donde se especifica dentro del fichero pom.xml en la etiqueta finalName. Este nombre se especifica dentro del fichero pom.xml.

Una vez construido el proyecto, ejecutamos el resultado en modo local:

    mvn clean jetty:run

viendo en la salida en el navegador el Hola Mundo!!.

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
