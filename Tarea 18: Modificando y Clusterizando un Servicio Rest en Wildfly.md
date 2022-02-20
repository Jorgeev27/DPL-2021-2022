# Tarea 18: Modificando y Clsuterizando un Servicio REST en Wildfly

  ## Jorge Escobar Viñuales

  ## Indice:
 - Creación del Servicio

 ### 1. CREACIÓN DEL SERVICIO

La estructura del proyecto será la siguiente:

Y para empezar, creamos el fichero docker-compose.yml:

El siguiente paso, será crear el archivo Dockerfile:

Una vez realizado, creamos el archivo data.sql:

Y, por último, creamos el archivo index.php:

Ya realizado todos los archivos y con sus configuraciones, hacemos el siguiente comando:

    sudo docker-compose up -d

Tuve que volver a realizar el comando porque me daba error en la BBDD y como estaba predeterminado el puerto en 3306, tuve que cambio a 3310:

Ya con los cambios, se realiza la imagen perfecta.

El siguiente paso será verificar si las imágenes de Wildfly están funcionando correctamente:

Y comprobamos PHPMyAdmin:

Y nos logueamos correctamente:
