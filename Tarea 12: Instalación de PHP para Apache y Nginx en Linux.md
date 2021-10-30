# Tarea 12: Instalación de PHP para Apache y Nginx en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - PHP para Apache
 - PHP para Nginx
 - Probar PHP en Ubuntu

Previamente, para instalar PHP debemos actualizar las listas de paquetes. Para ello, utilizaremos el comando:

    sudo apt update

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%201.png)

 ### 1. PHP PARA APACHE

Si se usa Apache como servicio web, el paquete que se necesita será libapache2-mod-php. Para ello, utilizaremos este comando para instalar PHP:

    sudo apt install -y php

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%202.png)

  ### 2. PHP PARA NGINX

Si se usa Nginx como servicio web, el paquete que se necesita será php-fpm. Para ello, utilizaremos este comando para instalar PHP:

    sudo apt install -y php-fpm

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%203.png)

En este caso, se instala PHP como servicio independiente, el servicio php7.4-fpm.service o php7.4-fpm, que queda iniciado y habilitado para su arranque automático junto a Ubuntu.

Será necesario configurar Nginx para conectar con el servicio PHP-FPM, editando el archivo de configuración. Para ello, utilizaremos el comando:

    sudo nano /etc/nginx/sites-available/default

Buscamos y activamos la sección location con la configuración adecuada, en este caso correspondiente al servicio PHP-FPM:

    ...
                # pass PHP scripts to FastCGI server
                #
                location ~ \.php$ {
                        include snippets/fastcgi-php.conf;
                #
                #       # With php-fpm (or other unix sockets):
                        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
                #       # With php-cgi (or other tcp sockets):
                #       fastcgi_pass 127.0.0.1:9000;
                }
    ...

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%204.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%205.png)

Y recargamos la configuración de Nginx:

    sudo systemctl reload nginx

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%206.png)

También se incluye otras dependencias de PHP: para consola, o PHP CLI, con el que se puede comprobar en cualquier momento la versión que se tiene instalada en nuestro Ubuntu, usando el comando:

    php -v

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%207.png)

  ### 3. PROBAR PHP EN UBUNTU

Para probar PHP en Ubuntu, crearemos un pequeño archivo accesible vía web. Para ello, utilizaremos el comando:

    sudo nano /var/www/html/info.php

Y el contenido será únicamente esta línea:

    <?php 
        phpinfo(); 
    ?>

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%208.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%209.png)

Y desde el navegador accederemos utilizando la dirección IP o dominio del servidor Ubuntu, añadiendo la ruta /info.php.

Habrá que llevar la misma configuración a los subdominios que se hayan creado anteriormente en otras tareas.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%2010.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2012%20-%20Instalaci%C3%B3n%20de%20PHP%20en%20Linux/PHP%2012.png)

Profe, he intentado la manera de arreglar el error de que no me sale la página de info.php
pero no he encontrado resultado.
