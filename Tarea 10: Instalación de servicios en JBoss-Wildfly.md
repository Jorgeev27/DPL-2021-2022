# Tarea 10: Instalación de servicios en JBoss-Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Requisitos Previos
 - Pasos para realizar los servicios rs/ws en JBoss-Wildfly

 ### 1. REQUISITOS PREVIOS

Se necesita una máquina virtual Ubuntu, con la instalación previamente realizada de JAVA y MAVEN. Además de esto, la instalación JBoss-Wildfly y desplegado el servidor de aplicaciones de este último.

  ### 2. PASOS PARA REALIZAR LOS SERVICIOS RS/WS EN JBOSS-WILDFLY

INSTALACIÓN DEL SERVICIO HELLO-RS:

Para realizar la siguiente actividad, se necesita descargar los ejemplos de Github de Wildfly quickstart ejemplos. Una vez descargado, accedemos al directorio de helloworld-rs y ejecutar el comando:

    mvn clean install

Una vez realizada toda la compilación, accedemos al servidor de Wildfly y seleccionamos el apartado de Deployments; pulsamos en la pestaña +, y seleccionamos la carpeta del proyecto helloworld-rs (en concreto el archivo helloworld-rs.war dentro de la carpeta _helloworld-rs/target/). Ya desplegado el archivo helloworld-rs.war, accedemos a la url de nuestro servidor (localhost o Dirección IP:8084/helloworld-rs), y voila: despliegue correcto del servicio.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%201.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%202.png)

INSTALACIÓN DEL SERVICIO HELLO-WS:

Se necesita descargar los ejemplos de Github de Wildfly quickstart ejemplos. Una vez descargado, accedemos al directorio de helloworld-ws y ejecutar el comando:

    mvn clean install

Una vez realizada toda la compilación, accedemos al servidor de Wildfly y seleccionamos el apartado de Deployments; pulsamos en la pestaña +, y seleccionamos la carpeta del proyecto helloworld-ws (en concreto el archivo helloworld-ws.war dentro de la carpeta _helloworld-ws/target/). Ya desplegado el archivo helloworld-rs.war, accedemos a la url de nuestro servidor (localhost o Dirección IP:8084/helloworld-ws), y voila: despliegue correcto del servicio.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%203.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%204.png)

DESPLIEGUE DEL SERVICIO HELLO-RS:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%205.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%206.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%207.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%208.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2010.png)

DESPLIEGUE DEL SERVICIO HELLO-WS:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2012.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2013.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2014.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2010%20-%20Instalaci%C3%B3n%20de%20servicios%20JBoss-Wildfly/Servicio%20JBoss-Wildfly%2015.png)
