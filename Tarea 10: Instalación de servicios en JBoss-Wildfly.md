# Tarea 10: Instalación de servicios en JBoss-Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Requisitos Previos
 - Pasos para realizar los servicios rs/ws en JBoss-Wildfly

 ### 1. REQUISITOS PREVIOS

Se necesita una máquina virtual Ubuntu, con la instalación previamente realizada de JAVA y MAVEN. Además de esto, la instalación JBoss-Wildfly y desplegado el servidor de aplicaciones de este último.

  ### 2. CREANDO NUESTRO SERVICIO RESTFUL API

INSTALACIÓN DEL SERVICIO HELLO-RS:

Para realizar la siguiente actividad, se necesita descargar los ejemplos de Github de Wildfly quickstart ejemplos. Una vez descargado, accedemos al directorio de helloworld-rs y ejecutar el comando:

    mvn clean install

Una vez realizada toda la compilación, accedemos al servidor de Wildfly y seleccionamos el apartado de Deployments; pulsamos en la pestaña +, y seleccionamos la carpeta del proyecto helloworld-rs (en concreto el archivo helloworld-rs.war dentro de la carpeta _helloworld-rs/target/). Ya desplegado el archivo helloworld-rs.war, accedemos a la url de nuestro servidor (localhost o Dirección IP:8084/helloworld-rs), y voila: despliegue correcto del servicio.


INSTALACIÓN DEL SERVICIO HELLO-WS:

Se necesita descargar los ejemplos de Github de Wildfly quickstart ejemplos. Una vez descargado, accedemos al directorio de helloworld-ws y ejecutar el comando:

    mvn clean install

Una vez realizada toda la compilación, accedemos al servidor de Wildfly y seleccionamos el apartado de Deployments; pulsamos en la pestaña +, y seleccionamos la carpeta del proyecto helloworld-ws (en concreto el archivo helloworld-ws.war dentro de la carpeta _helloworld-ws/target/). Ya desplegado el archivo helloworld-rs.war, accedemos a la url de nuestro servidor (localhost o Dirección IP:8084/helloworld-ws), y voila: despliegue correcto del servicio.

DESPLIEGUE DEL SERVICIO HELLO-RS:

DESPLIEGUE DEL SERVICIO HELLO-WS:
