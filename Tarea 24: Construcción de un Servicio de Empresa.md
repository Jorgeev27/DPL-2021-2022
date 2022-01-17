# Tarea 23: Instalación Servidor FTP en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Dominio Principal
 - Subdominio con Info.php
 - Base de datos - PHPMyAdmin
 - SFTP

Necesitamos resolver el problema de una construcción del servicio de una empresa cualquiera y, para ello, debemos realizar los siguientes pasos para llevar una solución para este hecho.

 ### 1. DOMINIO PRINCIPAL

 En primer lugar, necesitamos el dominio principal de nuestra empresa, en este caso, nuestro dominio se llamará www.jorgeevsystem.com.

 Mi primer paso, fue hacer un directorio en /var/www llamado jorgeevsystem. Dentro de ese directorio (jorgeevsystem), creamos dos directorios más (html y subdomain, que este último será el segundo punto de la explicación). Dentro del directorio /var/www/jorgeevsystem/html, creamos un fichero llamado index.php donde tendremos la página inicial.

 El segundo paso, será ir a /etc/apache2/sites-available/ y copiamos el fichero default que nos viene del servidor Apache y lo llamamos jorgeevsystem.conf. Una vez realizados todos los ajustes, habilitamos este archivo en sites-enabled de Apache.

 El tercer paso, será ir al fichero /etc/hosts y ponemos nuestro dominio: www.jorgeevsystem.com

 Con todos estos pasos, nuestro dominio principal estará funcionando correctamente.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%201.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%202.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%204.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%205.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%206.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%208.png)

 ### 2. SUBDOMINIO CON INFO.PHP

 Tras realizar el primer punto de la tarea, nuestro siguiente punto será realizar un subdominio con PHP instalado y que se muestre info.php.

 Para ello, realizamos los siguientes pasos: nos vamos al directorio /var/www/jorgeevsystem y creamos un directorio dentro llamado subdomain. Dentro de ese directorio (/var/www/jorgeevsystem/subdomain), creamos info.php donde ponemos el phpinfo.

 Una vez hecho esto, nos vamos al archivo jorgeevsystem.conf que está en /etc/apache2/sites-available/, y lo editamos para crear un Alias y así tener el subdominio.

 Ya con el Alias creado, reiniciamos Apache y nos dirigimos a nuestra página: www.jorgeevsystem.com/subdomain y ahí tendremos el archivo de info.php donde tendremos toda nuestra información acerca de PHP.
 
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%203.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%207.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%2010.png)

 ### 3. BASE DE DATOS - PHPMYADMIN

 Para la base de datos y PHPMyAdmin, haremos los mismos pasos que los anteriores. Generamos un archivo de configuración, el que tenemos que añadir el Alias para el servidor.

 Una vez realizado, creamos un directorio en la estructura del proyecto y se comprueba su funcionamiento. Iniciando sesión y veremos las bases de datos.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%2012.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2024%20-%20Construcci%C3%B3n%20de%20un%20Servicio%20de%20Empresa/DPL%20Empresa%2013.png)

 ### 4. SFTP

 Para realizar el subdominio SFTP, realizamos los mismos que los anteriores: generando un archivo de configuración, poniendo el Alias para que funcione en el servidor.

 Ya realizado, usaremos Filezilla para transferir un fichero cualquiera y comprobamos dicha transferencia en nuestro servidor.
