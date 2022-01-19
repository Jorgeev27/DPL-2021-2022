# Tarea 26 - Instalación y configuración de Jenkins en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalación de Jenkins en Docker
 - Instalación de Jenkins en Docker-Compose

 ### 1. INSTALACIÓN DE JENKINS EN DOCKER

Para esta ocasión, hacemos el mismo proceso de la actividad anterior (el dominio y su configuración):


Y una vez eso, nos descargamos la imagen de Jenkins para Docker, con el comando:

    docker pull jenkins/jenkins:lts

Y verificamos la imagen para saber si se ha descargado correctamente, con el comando:

    sudo docker images

Ahora ejecuta Jenkins como contenedor Docker poniéndolo en el puerto 8080, con el comando:

    docker run -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins/jenkins:lts

Y ya tenemos Jenkins corriendo con Docker.

 ### 2. INSTALACIÓN DE JENKINS EN DOCKER-COMPOSE

Ahora, haremos instalar la imagen de Jenkins con Docker-Compose. Por lo tanto haremos los siguientes archivos:

Dockerfile, conteniendo las instrucciones para construir la imagen:

    FROM jenkins/jenkins

    USER root
    RUN apt-get -y update && apt-get install -y maven

    USER jenkins
    COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
    RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

En la línea 1, la imagen base. En la línea 4, instalamos Maven; indicando el usuario de ejecución es el root en la línea 3 y los nuevos usuarios de ejecución en la línea 6. En la línea 7, copiamos el fichero plugins.txt, y en la última línea se ejecuta el script install-plugins.sh que toma la lista de plugins del archivo plugins.txt y los instala en Jenkins.

Plugins.txt, incluyendo cada plugin que queremos que se instale en Jenkins:

    ace-editor
    ant
    antisamy-markup-formatter
    apache-httpcomponents-client-4-api
    authentication-tokens
    branch-api
    build-monitor-plugin
    build-pipeline-plugin
    cloudbees-folder
    conditional-buildstep
    copyartifact  
    credentials
    credentials-binding
    deploy
    display-url-api
    docker-commons
    docker-workflow
    durable-task
    git
    github
    github-api
    git-client
    git-server
    gradle
    greenballs
    handlebars
    jackson2-api
    javadoc
    jquery
    jquery-detached
    jsch
    junit
    mailer
    matrix-project
    maven-plugin
    momentjs
    nested-view
    parameterized-trigger
    pipeline-build-step
    pipeline-graph-analysis
    pipeline-input-step
    pipeline-milestone-step
    pipeline-model-api
    pipeline-model-declarative-agent
    pipeline-model-definition
    pipeline-model-extensions
    pipeline-rest-api
    pipeline-stage-step
    pipeline-stage-tags-metadata
    pipeline-stage-view
    plain-credentials
    run-condition
    scm-api
    script-security  
    ssh-credentials
    structs
    token-macro
    workflow-aggregator
    workflow-api
    workflow-basic-steps
    workflow-cps
    workflow-cps-global-lib
    workflow-durable-task-step
    workflow-job
    workflow-multibranch
    workflow-scm-step
    workflow-step-api
    workflow-support

Docker-compose.yml:

    version: '3'
    services:
      master:
        build: jenkins
        image: dpl/jenkins:latest
        restart: unless-stopped
        hostname: jenkins
        ports:
          - "8080:8080"
          - "50000:50000"
        volumes:
          - jenkins_home:/var/jenkins_home

    volumes:
      jenkins_home:

En la línea 4 indicamos el directorio en la que se va a construir la imagen; un subdirectorio de donde se encuentra el fichero docker-compose.yml; en la línea 5 indicamos el nombre de la imagen, en este caso, la dejamos como está predeterminada (dpl/jenkins:latest); en la línea 6 reiniciamos el contenedor a menos que se detenga explícitamente o que Docker lo detenga o reinicie; en las líneas 9-10 indicamos el hostname del contenedor; en las líneas 12-13-14-15 definimos el volumen jenkins_home, que utiliza los cambios que realizamos en la configuración de Jenkins persista tras la destrucción del contenedor.

Una vez realizado, procedemos a construir la imagen, con el comando:

    docker-compose build

Para arrancar el contenedor, utilizamos el comando:

    docker-compose up -d

Y ya con esto, tenemos la imagen creada. Así que accederemos nuestro dominio:8080 para entrar en la consola de administración de Jenkins.

Y si queremos ver la contraseña del usuario admin, utilizamos el comando:

    docker exec -it dockerjenkins_master_1 cat /var/jenkins_home/secrets/initialAdminPassword
