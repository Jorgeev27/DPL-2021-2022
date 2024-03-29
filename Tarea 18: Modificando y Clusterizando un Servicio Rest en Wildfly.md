# Tarea 18: Modificando y Clsuterizando un Servicio REST en Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Creación del Servicio

 ### 1. CREACIÓN DEL SERVICIO

La estructura del proyecto será la siguiente:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%201.png)

Y para empezar, creamos el fichero docker-compose.yml:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%202.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%203.png)

El siguiente paso, será crear el archivo Dockerfile:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%204.png)

Una vez realizado, creamos el archivo data.sql:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%205.png)

Y, por último, creamos el archivo index.php:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%206.png)

Ya realizado todos los archivos y con sus configuraciones, hacemos el siguiente comando:

    sudo docker-compose up -d

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%207.png)

Tuve que volver a realizar el comando porque me daba error en la BBDD y como estaba predeterminado el puerto en 3306, tuve que cambio a 3310:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%208.png)

Ya con los cambios, se realiza la imagen perfecta.

El siguiente paso será verificar si las imágenes de Wildfly están funcionando correctamente:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%2010.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%2011.png)

Y comprobamos PHPMyAdmin:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%2012.png)

Y nos logueamos correctamente:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2018%20-%20Modificando%20y%20Clusterizando%20un%20servicio%20REST%20en%20Wildfly/Wildfly%20REST%2013.png)
