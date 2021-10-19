# Tarea 8: Despliegue de un Servicio REST en Apache-Tomcat

  ## Jorge Escobar Viñuales

  ## Indice:
 - Introducción
 - Creando nuestro servicio RESTFUL API
 - Despliegue del servicio

 ### 1. INTRODUCCIÓN

 Si se quiere utilizar JAX-RS para crear servicios RESTful, podemos ayudarnos por una implementación que hizo Jersey de estándar JAX-RS(JSR 311    o JSR 339). Ahora, necesitamos un servidor para desplegar la aplicación y utilizaremos Tomcat 10.

 Así que veamos que pasos hay que dar para poder crear servicios RESTful con Tomcat y Jersey. En todo el proceso de la creación de nuestra app JAVA con servicios RESTful nos vamos a apoyar en MAVEN como gestor de dependencias.

 Una API REST se aprovecha los métodos HTTP descritos en el protocolo RFC 2616. Se utiliza las solicitudes:

  - GET: buscar datos
  - PUT: alterar el estado de los datos (como objeto, archivo, bloque),
  - POST: crear datos.
  - DELETE: métodos para eliminar. Se ven diferentes códigos de estado HTTP utilizados por las API REST.

  ### 2. CREANDO NUESTRO SERVICIO RESTFUL API

Los requisitos que necesitamos para crear el servicio RESTful, debemos tener instalado JAVA, MAVEN y tener hecho la aplicación del proyecto de la app en JAVA.

  ### 3. DESPLIEGUE DEL SERVICIO

  Esta tarea tiene como objetivo el despliegue del servicio en el servidor Tomcat 10, tal y como se realizó con la tarea anterior del proyecto de la app en JAVA.

  El consumo del servicio se verifica a través de la url de nuestro servicio (http:localhost [O DIRECCIÓN IP]/rest/users), y se ataca con el cliente rest, como por ejemplo con ADVANCED REST CLIENT.

  Si se producen problemas durante el despliegue del servicio, podemos verificar el problema en los ficheros que se encuentrar alojado en la carpeta logs de Tomcat. Los ficheros se pueden prestar atención son:

  catalina_fecha
  localhost_fecha. Aquí, se mostrarán los problemas de acceso, dependencias de librerías, etc., como en el ejemplo siguiente:

    SEVERE [http-nio-8082-exec-6] org.apache.catalina.core.StandardContext.loadOnStartup Servlet [Jersey Web Application] in web application [/rest-service] threw load() exception
        java.lang.ClassNotFoundException: com.sun.jersey.spi.container.servlet.ServletContainer

  Para solventar el problema, debemos incluir las librerías en el WAR, dentro de la carpeta lib de Tomcat o dentro de la carpeta WEB-INFO/lib del propio proyecto.

  Se pueden hacer mejoras en el servicio, como por ejemplo una implementación de un nuevo método que permita realizar la búsqueda por el campo ahí, el cual hay que añadir en la clase User. Además, se debe implementar el método getUserByDni.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%208%20-%20Despliegue%20de%20un%20servicio%20REST%20en%20Apache-Tomcat/REST%201.png)

MVN Clean Install y me salen las dependencias del archivo.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%208%20-%20Despliegue%20de%20un%20servicio%20REST%20en%20Apache-Tomcat/REST%202.png)
Añadí dependencias pero que no han tenido éxito

Solamente, tengo estas capturas porque se me olvidó hacer capturas de lo que hice y demás. Además, con el consentimiento de BUSCAR EN INTERNET los famosos errores que nos ha dado pero, sin éxito.
