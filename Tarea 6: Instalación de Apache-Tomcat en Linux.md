# Tarea 6: Instalación de Apache-Tomcat en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Actualización de los repositorios
 - Instalación de Apache-Tomcat
 - Acceso

 Para poder realizar la actividad, se necesitará una máquina Linux.

 ### 1. ACTUALIZACIÓN DE LOS REPOSITORIOS

Antes de comenzar cualquier instalación de cualquier programa, se recomienda actualizar el repositorio del sistema operativo. De este modo, la instalación de Apache-Tomcat en cualquier Ubuntu es siempre segura y actualizada

Para ello, utilizaremos estos dos comandos:

    sudo apt update

    sudo apt upgrade

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%201.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%202.png)

  ### 2. INSTALACIÓN DE APACHE-TOMCAT

Vamos a descargar Tomcat10 a través de la página oficial o ejecutar el siguiente comando y se descarga:

    wget https://downloads.apache.org/tomcat/tomcat-10/v10.0.12/bin/apache-tomcat-10.0.12.tar.gz

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%203.png)

Vamos a instalar Tomcat10, primeramente creamos un usuario tomcat:

    sudo useradd -U -m -d /opt/tomcat -k /dev/null -s /bin/false tomcat

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%204.png)

Descomprimimos el paquete en su ubicación definitiva:

    sudo tar xf apache-tomcat-10.0.12.tar.gz -C /opt/tomcat/

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%205.png)

Asignamos como propietario de los archivos de Tomcat10 el usuario tomcat que creamos:

    sudo chown -R tomcat: /opt/tomcat/

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%206.png)

Renombramos el directorio de instalación. Como el directorio de Tomcat10 tiene los números de la versión, se crea un enlace simbólico sin números:

    sudo ln -s /opt/tomcat/apache-tomcat-10.0.12/ /opt/tomcat/apache-tomcat

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%207.png)

Configuramos e iniciamos el servicio de Tomcat10. Para ello, creamos un archivo de unidad para Systemd:

    sudo nano /etc/systemd/system/tomcat10.service

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%208.png)

Y el contenido es el siguiente:

    [Unit]
    Description=Tomcat 10.0 servlet container para Ubuntu 20.04 LTS
    After=network.target
    [Service]
    Type=forking
    User=tomcat
    Group=tomcat
    Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
    Environment="CATALINA_BASE=/opt/tomcat/apache-tomcat"
    Environment="CATALINA_HOME=/opt/tomcat/apache-tomcat"
    Environment="CATALINA_PID=/opt/tomcat/apache-tomcat/temp/tomcat.pid"
    Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
    ExecStart=/opt/tomcat/apache-tomcat/bin/startup.sh
    ExecStop=/opt/tomcat/apache-tomcat/bin/shutdown.sh
    [Install]
    WantedBy=multi-user.target

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%291.png)

Guardamos el archivo e iniciamos el servicio de Tomcat10:

    sudo systemctl start tomcat10

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%2010.png)

Verificamos el estado del servicio de Tomcat10 para ver si está funcionando:

    systemctl status tomcat10

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%2011.png)

Si se quiere iniciar automáticamente Tomcat10, habilitamos el servicio:

    sudo systemctl enable tomcat10

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%2012.png)

    ### 3. ACCESO A APACHE-TOMCAT

Por defecto, Tomcat10 se inicia en el puerto de conexión 8080, pero anteriormente instalamos GitLab; entonces tendremos problemas a la hora de acceder a Apache-Tomcat. Para ello, configuraremos el archivo server.xml que está en la carpeta de apache-tomcat, conf y encontraremos ahí el archivo server.xml:

    cd /apache-tomcat-10.0.12/conf/

Desde conf:

    sudo nano server.xml

Cambiamos el puerto de 8080:

    <Connector port="8080"       //Change this
                protocol="HTTP/1.1"
                connectionTimeout="20000"
                redirectPort="8443"
                />



A 8082:

    <Connector port="8080"       //Change this
                protocol="HTTP/1.1"
                connectionTimeout="20000"
                redirectPort="8443"
                />

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%2013.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%206%20-%20Instalaci%C3%B3n%20de%20Apache-Tomcat%20en%20Linux/Apache%20Tomcat%2014.png)
