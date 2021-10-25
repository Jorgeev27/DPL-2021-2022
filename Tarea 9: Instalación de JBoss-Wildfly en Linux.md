# Tarea 9: Instalación de JBoss-Wildfly en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Actualización de los repositorios
 - Instalación de JBoss-Wildfly
 - Acceso a JBoss-Wildfly

Para poder realizar la actividad, se necesitará una máquina Linux e instalado previamente MAVEN y JAVA instalado.

 ### 1. ACTUALIZACIÓN DE LOS REPOSITORIOS

Antes de comenzar cualquier instalación de cualquier programa, se recomienda actualizar el repositorio del sistema operativo. De este modo, la instalación de JBoss-Wildfly en cualquier Ubuntu es siempre segura y actualizada.

Para ello, utilizaremos estos dos comandos:

    sudo apt update

    sudo apt upgrade
    
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%201.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%202.png)

  ### 2. INSTALACIÓN DE JBOSS-WILDFLY

Vamos a descargar JBoss-Wildfly a través de la página oficial o ejecutar el siguiente comando y se descarga:

    wget https://github.com/wildfly/wildfly/releases/download/25.0.0.Final/wildfly-25.0.0.Final.zip

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%203.png)

Vamos a instalar JBoss-Wildfly, primeramente creamos un usuario wildfly:

    sudo groupadd -r wildfly
    sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%204.png)

Descomprimimos el paquete en su ubicación definitiva:

    sudo tar xf /tmp/wildfly-25.0.0.Final.zip -C /opt/

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%205.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%206.png)

Creamos un enlace simbólico al directorio:

    sudo ln -s /opt/wildfly-25.0.0.Final.zip /opt/wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%207.png)

Damos acceso al usuario y grupo wildfly:

    sudo chown -R wildfly: /opt/wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%208.png)

Configuramos e iniciamos el servicio de JBoss-Wildfly.:

    sudo mkdir -p /etc/wildfly

    sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/

    sudo nano /etc/wildfly/wildfly.conf

    **WILDFLY_BIND=0.0.0.0**

    sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/

    sudo sh -c 'chmod +x /opt/wildfly/bin/*.sh'

    sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/

    sudo systemctl daemon-reload

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2010.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2012.png)

Iniciamos el servicio. Una vez guardado el archivo, se puede iniciar el servicio con el siguiente comando:

    sudo systemctl start wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2013.png)

Verificamos el estado del servicio de JBoss-Wildfly para ver si está funcionando:

    sudo systemctl status wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2014.png)

Inicio automático del servicio de wildfly. Si queremos que arranque automáticamente en cada encendido de la máquina virtual, tendremos que habilitar el servicio:

    sudo systemctl enable wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2015.png)

Vamos a permitir el tráfico del puerto. Hemos modificado el puerto 8080 por 8084, para ello se modifica la etiqueta del comando:

    sudo nano /opt/wildfly/standalone/configuration/standalone.xml
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2016.png)

Una vez dentro buscamos:

    <socket-binding name="http" port="${jboss.http.port:8080}"/>

por:

    <socket-binding name="http" port="${jboss.http.port:8084}"/>
    
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2017.png)

Y permitimos el tráfico con el puerto:

    sudo ufw allow 8083/tcp
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2018.png)

(Aquí me equivoqué y puse 8083 pero de todas maneras, me funciona igualmente).

  ### 3. DESPLIEGUE DEL SERVICIO

Para acceder a Wildfly desde el navegador, indicaremos la dirección del servidor (IP, nombre DNS del dominio, etc.) y el puerto 8084. Y tendremos Wildfly desplegado.

Para añadir usuarios a Wildfly, con capacidad de administrar las aplicaciones desplegadas, debemos hacer lo siguiente:

Crear un usuario administrador:

    sudo /opt/wildfly/bin/add-user.sh

Seleccionamos la opción A, indicando el usuario de gestión. Y obtendremos el siguiente mensaje:

    $ ./add-user.sh

    What type of user do you wish to add?
    a) Management User (mgmt-users.properties)
    b) Application User (application-users.properties)
    (a): a

    Enter the details of the new user to add.
    Using realm 'ManagementRealm' as discovered from the existing property files.
    Username : admin123
    Password recommendations are listed below. To modify these restrictions edit the add-user.properties configuration file.
    - The password should be different from the username
    - The password should not be one of the following restricted values {root, admin, administrator}
    - The password should contain at least 8 characters, 1 alphabetic character(s), 1 digit(s), 1 non-alphanumeric symbol(s)
    Password :
    Re-enter Password :
    What groups do you want this user to belong to? (Please enter a comma separated list, or leave blank for none)[  ]:
    About to add user 'admin123' for realm 'ManagementRealm'
    Is this correct yes/no? yes
    Added user 'admin123' to file
    value="UGFzc3dvcmQxMjM="
    ... />

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2019.png)

Debes de configurarlo según tus necesidades


Para gestionar la consola de forma remota, hay que realizar la siguiente configuración con el siguiente comando:

    sudo nano /etc/wildfly/wildfly.conf
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2020.png)

    WILDFLY_CONSOLE_BIND=0.0.0.0

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2021.png)

    sudo nano /opt/wildfly/bin/launch.sh

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2022.png)

lanzando así lo siguiente:

    $WILDFLY_HOME/bin/domain.sh -c $2 -b $3 -bmanagement $4

    else

    $WILDFLY_HOME/bin/standalone.sh -c $2 -b $3 -bmanagement $4

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2023.png)

La ejecución indica el modo en el que vamos a lanzar el servidor(standalone o damain).

Para finalizar, debemos realizar:

    sudo systemctl restart wildfly

    sudo nano /etc/systemd/system/wildfly.service

    ExecStart=/opt/wildfly/bin/launch.sh $WILDFLY_MODE $WILDFLY_CONFIG $WILDFLY_BIND $WILDFLY_CONSOLE_BIND

    sudo systemctl daemon-reload

    sudo systemctl restart wildfly

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2024.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2025.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2026.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2027.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%209%20-%20Instalaci%C3%B3n%20de%20JBoss-Wildfly%20en%20Linux/JBoss%20Wildfly%2028.png)
