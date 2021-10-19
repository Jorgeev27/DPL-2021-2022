# Tarea 7: Despliegue de WAR en Apache-Tomcat

  ## Jorge Escobar Viñuales

  ## Indice:
 - Estructura de Tomcat
 - Terminología
 - Creación de una app web en Java

Apache Tomcat es uno de los Web Server más importantes en la comunidad de Java. Y aquí, se verá el despliegue de una aplicación web.

 ### 1. ESTRUCTURA DE TOMCAT

Habrá que relacionarse con las carpetas más importantes de Tomcat.

$CATALINA_HOME: Punto de instalación de Tomcat.

$CATALINA_BASE: Directorio de despliegue de las apliaciones de Tomcat, y configurable. Además, debe ser asociada con $CATALINA_HOME. Dichas aplicaciones web son desplegadas en el directorio $CATALINA_HOME\webapps.

  ### 2. INSTALACIÓN DE APACHE-TOMCAT

Document root: Referencia de la carpeta superior de la aplicación web, donde están los recursos: .jsp, .html, .java e imágenes.

Context path: Referencia a la localización de la dirección del servidor y representa el nombre de la aplicación web. (EJEMPLO: Si está desplegado en $CATALINA_HOME\webapps\myapp, el acceso de la aplicación debe ser hhtp://localhost/myapp, con el contexto de la aplicación /myapp.

War: Extensión de los ficheros que contienen la aplicación web, heredada de .zip de los comprimidos web. Se puede hacer a través del IDE o de herramientas como Maven que realizan esta construcción de ficheros, con su correspondiente despliegue automático.

EJEMPLO DE WAR:
    <plugin>
      <groupId>org.apache.tomcat.maven</groupId>
      <artifactId>tomcat7-maven-plugin</artifactId>
      <version>2.2</version>
      <configuration>
          <url>http://localhost:8082/manager/text</url>
          <server>TomcatServer</server>
          <path>/myapp</path>
          </configuration>
    </plugin>

El despliegue se realiza con el siguiente comando:

      mvn tomcat7:deploy

O también con el redespliegue con el comando:

      mvn tomcat7:redeploy

  O la eliminación de este, con el comando:

      mvn tomcat7:undeploy

  ### 3. ACCESO A APACHE-TOMCAT

Los requisitos son: tener realizada la instalación de JAVA, y también la de MAVEN.

Disponemos de un proyecto de una web en JAVA, donde se deben realizar los siguientes cambios:

En el fichero web.xml, sustituimos:

    <display-name>app-web-alumno</display-name>

por:

    <display-name>app-web-aron</display-name>
    
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%207%20-%20Despliegue%20de%20WAR%20en%20Apache-Tomcat/WAR%201.png)

Siendo así, aron el nombre del alumno (también, para distinguirlo con más precisión, poniendo el nombre y apellidos del alumno).

En el fichero index.jsp, se realizará la sustitución del valor alumno siguiendo el mismo patrón que el paso anterior.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%207%20-%20Despliegue%20de%20WAR%20en%20Apache-Tomcat/WAR%202.png)

Una vez realizado los 2 pasos anteriores, lanzamos el fichero con el comando:

    mvn clean install
    
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%207%20-%20Despliegue%20de%20WAR%20en%20Apache-Tomcat/WAR%203.png)

Dentro de la carpeta target, se debe encontrar un fichero de nombre app-web-demo.war. Este nombre se especifica dentro del fichero pom.xml.

No obstante, se puede hacer uso de maven para construcción de la aplicación web. Para ello, se utiliza el siguiente comando. Tras la ejecución del comando, cuando se descargan las librerías por primera vez, se tiene una aplicación web completa en JAVA, lo que conocemos todos como el primer programa de “Hola Mundo!!”:

    mvn archetype:generate -DgroupId=es.iespuerto.alumno -DartifactId=
    
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%207%20-%20Despliegue%20de%20WAR%20en%20Apache-Tomcat/WAR%204.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%207%20-%20Despliegue%20de%20WAR%20en%20Apache-Tomcat/WAR%205.png)

Me está dando error en el ManagerApp, ya que puse el usuario tomcat y la contraseña s3cret y me salta el error 403. Se lo puse en un mensaje por privado por si me podía ayudar en ello.
