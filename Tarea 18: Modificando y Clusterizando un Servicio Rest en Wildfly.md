# Tarea 18: Modificando y Clsuterizando un Servicio REST en Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Introducción
 - Aplicación a desplegar
 - Aplicación a desplegar (Opcional)

 ### 1. INTRODUCCIÓN

Una vez realizado las tareas anteriores, vamos a construir y desplegar una app, que requiere Wildfly, bajo una api REST y una BBDD.

Los requerimientos de la tarea es:

  - El uso de la imagen de Docker de WILDFLY, que vimos en la instalación de Wildfly en Docker.
  - Cluster de 3 nodos de WILDFLY, de forma similar a Cluster Wildfly.
  - Instalación de la BBDD y phpmyadmin, de forma similar a Cluster Wildfly.
  - Uso de Docker Compose, para especificar las necesidades de nuestro entorno.

 ### 2. APLICACIÓN A DESPLEGAR

Vamos a utilizar la aplicación que se encuentra en los ejemplos de WIldfly; la aplicación helloworld-rs.

  ### 3. APLICACIÓN A DESPLEGAR (OPCIONAL)

Se puede incluir el plugin de Jetty, en el proyecto "hola mundo" que utilizamos en anteriores tareas.

Para verificar que todo funciona correctamente en el entorno local, utilizamos el comando:

    mvn clean jetty:run

viendo la salida en el navegador:

    http://localhost:8082/{artifactld}/.
    (SALIDA EN XML): http://localhost:8082/{artifactld}/rest/xml
    (SALIDA EN JSON): http://localhost:8082/{artifactld}/rest/json

Además, habrá que construir un fichero Dockerfile y un fichero docker-compose.yml
