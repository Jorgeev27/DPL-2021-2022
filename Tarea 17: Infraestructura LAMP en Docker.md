# Tarea 17: Infraestructura LAMP en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Diagram Docker

 ### 1. DIAGRAM DOCKER

La estructura del proyecto tiene que ser similar a la que se nos muestra:


Después de crear esta estructura, procedemos a instalar PHP en la versión 8.0.0 de Apache.

Lo pondremos en el documento Dockerfile:

    FROM php:8.0.0-apache
    ARG DEBIAN_FRONTEND=noninteractive
    RUN docker-php-ext-install mysqli
    RUN apt-get update \
          && apt-get install -y libzip-dev \
          && apt-get install -y zlib1g-dev \
          && rm -rf /var/lib/apt/lists/* \
          && docker-php-ext-install zip

    RUN a2enmod rewrite

Después de ello, vamos a la configuración de Docker Compose. Y aquí encontramos 3 grandes bloques: www, db y phpmyadmin:

    version: "3.5"
    services:
          www:
          build: .
          ports:
          - "80:80"
          volumes:
          - ./www:/var/www/html
          links:
          - db
          networks:
          - default
          db:
          image: mysql:8.0
          ports:
          - "3306:3306"
          command: --default-authentication-plugin=mysql_native_password
          environment:
          MYSQL_DATABASE: dbname
          MYSQL_USER: root
          MYSQL_PASSWORD: test
          MYSQL_ROOT_PASSWORD: test
          volumes:
          - ./dump:/docker-entrypoint-initdb.d
          - ./conf:/etc/mysql/conf.d
          - persistent:/var/lib/mysql
          networks:
          - default
          phpmyadmin:
          image: phpmyadmin/phpmyadmin
          links:
          - db:db
          ports:
          - 8000:80
          environment:
          MYSQL_USER: root
          MYSQL_PASSWORD: test
          MYSQL_ROOT_PASSWORD: test
          volumes:
          persistent:

Los contenedores actúan como servicios. En esta configuración son 3:

www: los atributos son:

  build: se construye el dockerfile sobre el contenedor

  ports: mantiene el mismo puerto con el servicio internamente corriendo: 80 y expuesto hacia fuera.

  volumes: definición donde la sincronización entre 2 directorios o volumen de datos, para ello, se sincroniza /www con /var/www/html que se encuentra en el contenedor.

  links: quién podrá verse y compartir recursos en red, para ello es necesario que el servidor web esté conectado al sistema gestor de datos que se encuentra en el contenedor db.

  networks: define el nombre de la red por la cuál estará conectados los contenedores.

    www:
        build: .
        ports:
        - "80:80"
        volumes:
        - ./www:/var/www/html
        links:
        - db
        networks:
        - default

db: los atributos son:

  comentar que no tiene un atributo build, dando a entender que no es necesario instalar paquetes desde un dockerfile como si lo necesitaba el contenedor www.

  image: selecciona la de mysql en la versión 8.0.

  ports: mantiene el mismo puerto con que el servicio internamente está corriendo, en el 3306 y expuesto hacia fuera.

  command: funcional para que se inserte un comando, donde dicha instrucción será para habilitar la autenticación con la contraseña nativa de MYSQL.

  environment: aplicación de variables de entorno, donde el contenedor recibe 4 con el prefijo de MYSQL_, donde escribe el nombre de la base de datos, nombre de usuario y contraseña.

  volumes: aplica la definición donde la sincronización entre ficheros, así como la configuración y donde corre el dominio de MYSQL.

  networks: nombre de la red por el cual estará conectados los contenedores, para el default en este caso donde se puede conocer el contenedor www.

    db:
        image: mysql:8.0
        ports:
        - "3306:3306"
        command: --default-authentication-plugin=mysql_native_password
        environment:
        MYSQL_DATABASE: dbname
        MYSQL_USER: root
        MYSQL_PASSWORD: test
        MYSQL_ROOT_PASSWORD: test
        volumes:
        - ./dump:/docker-entrypoint-initdb.d
        - ./conf:/etc/mysql/conf.d
        - persistent:/var/lib/mysql
        networks:
        - default

phpmyadmin: los atributos son:

  image: selecciona la imagen de phpmyadmin/phpmyadmin.

  ports: diferente a los demás, porque internamente el servicio está funcionando con el puerto 80, pero al exponerlo se necesita hacer con el otro, puesto que se colisionaría con el puerto que tiene expuesto el contenedor del servidor web www. De este modo, expone el puerto 8000.

  links: se conecta con el contenedor de la db para tener acceso al sistema gestor de la base de datos.

  environment: aplicación de variables de entorno, donde el contenedor recibe 3 con el prefijo de MYSQL_, donde escribe el nombre de usuario, contraseña y contraseña del root.


    phpmyadmin:
        image: phpmyadmin/phpmyadmin
        links:
        - db:db
        ports:
        - 8000:80
        environment:
          MYSQL_USER: root
          MYSQL_PASSWORD: test
          MYSQL_ROOT_PASSWORD: test

Este es el .sql que se importa a MYSQL.

    SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
    SET time_zone = "+00:00";

                   /*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
                   /*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
                   /*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
                   /*!40101 SET NAMES utf8mb4 */;

                   CREATE TABLE `Data` (
                     `id` int(11) NOT NULL,
                     `name` varchar(20) NOT NULL
                   ) ENGINE=InnoDB DEFAULT CHARSET=latin1;

                   INSERT INTO `Data` (`id`, `name`) VALUES (1, 'OpenWebinars Article'), (2, 'Crashell'), (3, 'Jerson Martinez'), (4, 'Antonio Moreno');

                   /*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
                   /*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
                   /*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

Y posteriormente, el código PHP ubicado en www/index.php:

    <html>
        <head>
        <title>Welcome to LAMP Infrastructure</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
        <script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
        </head>
        <body>
            <div class="container-fluid">
                <img src="https://manolohidalgo.com/wp-content/uploads/2020/10/fondo-despliegue2.jpg" alt="despliegues app web">
                <?php
                    echo "<h1>¡Hola, soy Alumno y te da la bienvenida!</h1>";

                    $conn = mysqli_connect('db', 'root', 'test', "dbname");
                    $query = 'SELECT * From Data';
                    $result = mysqli_query($conn, $query);

                    echo '<table class="table table-striped">';
                    echo '<thead><tr><th></th><th>id</th><th>name</th></tr></thead>';
                    while($value = $result->fetch_array(MYSQLI_ASSOC)){
                        echo '<tr>';
                        echo '<td><a href="#"><span class="glyphicon glyphicon-search"></span></a></td>';
                        foreach($value as $element){
                            echo '<td>' . $element . '</td>';
                        }

                        echo '</tr>';
                      }
                      echo '</table>';

                      $result->close();
                      mysqli_close($conn);
                  ?>
              </div>
          </body>
    </html>

Para lanzar la configuración, ejecutamos el comando:

    sudo docker-compose up-d

Para verificar los contenedores corriendo desde Docker Compose se ejecutan con el comando:

    sudo docker-compose ps

Ahora, probamos con el navegador y escribimos 127.0.0.1 para comprobar si se ha abierto correctamente. También podemos ir a 127.0.0.1:8000 para llegar al contenedor de phpmyadmin. De ahí, nos pedirá el usuario y contraseña:

    Usuario: root
    Contraseña: test

Y a partir de aquí, comprobamos si la base de datos está en phpmyadmin.

También, podemos verificar si está arrancado haciendo 127.0.0.1/index.php.

Y para parar Docker Compose, ejecutamos:

    docker-compose stop
