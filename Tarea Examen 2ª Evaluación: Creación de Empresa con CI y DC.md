# Tarea Examen 2ª Evaluación: Creación de Empresa con CI y DC

  ## Jorge Escobar Viñuales

  ## Indice:
 - Creación del Dominio de la Página
 - Creación del Dominio de SFTP
 - Creación del Dominio de Despliegue
 - Verificación de SFTP en Cliente; Subdominio Despliegue
 - Creación del Dominio de Jenkins
 - Creación del Dominio de PHPMyAdmin
 - Creación del Pipeline del Servicio de la Empresa

 ### 1. CREACIÓN DEL DOMINIO DE LA PÁGINA

Para ello, tendremos que ir a /etc/apache2/sites-available/ y creamos una nueva configuración llamada jorgeevsystem.conf:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%201.png)

Y haremos el comando:

    sudo a2ensite jorgeevsystem.conf

Para que esté configurado en /etc/apache2/sites-enabled/. Una vez realizado, recargamos el servicio de Apache2 con el comando:

    sudo systemctl reload apache2 

Una vez creado, nos iremos a /var/www/ y creamos el directorio jorgeevsystemExamen. Ya creado, dentro creamos otro directorio llamado html para crear el index.php:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%202.png)

Para que el dominio esté funcionando, nos iremos a /etc/hosts, y añadimos nuestro dominio.

Y ya con esto, tenemos creado nuestro dominio www.jorgeevsystem.com

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%203.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%204.png)

 ### 2. CREACIÓN DEL DOMINIO DE SFTP

Para ello, tendremos que ir a /etc/apache2/sites-available/ y creamos una nueva configuración llamada sftpjorgeevsystem.conf:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%205.png)

Y haremos el comando:

    sudo a2ensite sftpjorgeevsystem.conf

Para que esté configurado en /etc/apache2/sites-enabled/. Una vez realizado, recargamos el servicio de Apache2 con el comando:

    sudo systemctl reload apache2

Para que el dominio esté funcionando, nos iremos a /etc/hosts, y añadimos nuestro dominio.

Y ya con esto, tenemos creado nuestro dominio www.sftp.jorgeevsystem.com

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%206.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%207.png)

 ### 3. CREACIÓN DEL DOMINIO DE DESPLIEGUE

Para ello, tendremos que ir a /etc/apache2/sites-available/ y creamos una nueva configuración llamada desplieguejorgeevsystem.conf:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%208.png)

Y haremos el comando:

    sudo a2ensite desplieguejorgeevsystem.conf

Para que esté configurado en /etc/apache2/sites-enabled/. Una vez realizado, recargamos el servicio de Apache2 con el comando:

    sudo systemctl reload apache2

Para que el dominio esté funcionando, nos iremos a /etc/hosts, y añadimos nuestro dominio.

Y ya con esto, tenemos creado nuestro dominio www.despliegue.jorgeevsystem.com

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2010.png)

 ### 4. VERIFICACIÓN DE SFTP EN CLIENTE; SUBDOMINIO DESPLIEGUE

En este paso, creamos el usuario examen con el siguiente comando:

    sudo adduser –shell /bin/false/ examen

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2011.png)

Una vez creado, le asignamos como propietario en la carpeta despliegue de nuestro dominio; esta carpeta se encuentra creada en /var/www/jorgeevsystemExamen/.. Y para ello, usamos el comando:

    sudo chown examen:despliegue /var/www/jorgeevsystemExamen/despliegue

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2012.png)

Y ponemos en la carpeta de ese usuario como home con el comando:

    sudo usermod -d /var/www/jorgeevsystemExamen/despliegue examen

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2013.png)

Después, mediante Filezilla accedemos al servidor que queremos acceder (sftp.jorgeevsystem.com), con el usuario, contraseña que hemos creado de SFTP:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2014.png)

Ya con la conexión realizada, le añadimos los permisos 755. Y subimos un archivo como ejemplo; y se ha subido y realizado correctamente:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2015.png)

Ahora, mediante el navegador, comprobamos si ese archivo que se ha subido es el que se ha subido correctamente:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2016.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2017.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2018.png)

 ### 5. CREACIÓN EL DOMINIO DE JENKINS

Para ello, tendremos que ir a /etc/apache2/sites-available/ y creamos una nueva configuración llamada jenkinsjorgeevsystem.conf:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2019.png)

Y haremos el comando:

    sudo a2ensite jenkinsjorgeevsystem.conf

Para que esté configurado en /etc/apache2/sites-enabled/. Una vez realizado, recargamos el servicio de Apache2 con el comando:

    sudo systemctl reload apache2

Para que el dominio esté funcionando, nos iremos a /etc/hosts, y añadimos nuestro dominio.

Y ya con esto, tenemos creado nuestro dominio www.jenkins.jorgeevsystem.com

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2020.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2021.png)

 ### 6. CREACIÓN EL DOMINIO DE PHPMYADMIN

Para ello, tendremos que ir a /etc/apache2/sites-available/ y creamos una nueva configuración llamada phpmyadminjorgeevsystem.conf:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2022.png)

Y haremos el comando:

    sudo a2ensite phpmyadminjorgeevsystem.conf

Para que esté configurado en /etc/apache2/sites-enabled/. Una vez realizado, recargamos el servicio de Apache2 con el comando:

    sudo systemctl reload apache2

Para que el dominio esté funcionando, nos iremos a /etc/hosts, y añadimos nuestro dominio.

Y ya con esto, tenemos creado nuestro dominio www.phpmyadmin.jorgeevsystem.com

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2023.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2024.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2025.png)

 ### 7. CREACIÓN DEL PIPELINE DEL SERVICIO DE LA EMPRESA

Entraremos a Jenkins mediante el dominio que creamos anteriormente (jenkins.jorgeevsystem.com:8080).

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2026.png)

Y crearemos una nueva tarea, llamada ServicioEmpresaExamen y el tipo Pipeline:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2027.png)

Se nos mostrará la ventana de configuración del Pipeline, y creamos el siguiente script:

 - En la línea 6, subiremos el fichero index.php a sftp.jorgeevsystem.com, que lo veremos disponible en despliegue.jorgeevsystem.com

 - En la línea 11, la versión instalada de MySQL.

 - En la línea 12, la frase que queremos buscar; en este caso, con el comando grep ‘Pagina inicial de Jorge Escobar System’.

 - En la línea 13, con el comando grep buscamos la versión que tenemos instalada de PHP.

 - En la línea 14, con el comando grep buscamos si está PHPMyAdmin.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2028.png)

Ya con todo configurado y creado, ejecutamos el Pipeline. PERO, nos dará en principio un error en los log.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2029.png)

Un error de la contraseña hace que tengamos el error; para solucionarlo creamos el archivo index.php en el Escritorio, y en la línea 6 del script, ponemos la dirección donde se encuentra el archivo para que este lo reciba sftp.jorgeevsystem.com.

Volvemos a ejecutar el Pipeline, y voilá: Tenemos el Pipeline corriendo y funcionando correctamente!!!.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2030.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%20Examen%202%C2%AA%20Evaluaci%C3%B3n%20-%20Creaci%C3%B3n%20de%20Empresa%20con%20CI%20y%20DC/Examen%20DPL%2031.png)
