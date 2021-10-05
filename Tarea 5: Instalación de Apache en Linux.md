# Tarea 5: Instalación de Apache en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Actualización de los repositorios
 - Instalación de paquetes adicionales
 - Instalación de Apache
 - Acceso

 Para poder realizar la actividad, se necesitará una máquina Linux.

 ### 1. ACTUALIZACIÓN DE LOS REPOSITORIOS

Antes de comenzar cualquier instalación de cualquier programa, se recomienda actualizar el repositorio del sistema operativo. De este modo, la intalación de GitLab en cualquier Ubuntu es siempre segura y actualizada

Para ello, utilizaremos estos dos comandos:

    sudo apt update

    sudo apt upgrade

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%201.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%202.png)

  ### 2. INSTALACIÓN DE APACHE
Ejecutar el siguiente comando para instalar Apache;

    sudo apt install apache2


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%203.png)

Nos mostrará el siguiente problema:

    apache2.service: Control process exited, code=exited, status=1/FAILURE
    systemd[1]: apache2.service: Failed with result 'exit-code'.
    systemd[1]: Failed to start The Apache HTTP Server.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%204.png)

El movido es lo siguiente:

    (98)Address already in use: AH00072: make_sock: could not bind to address 0.0.0.0:80

Una vez hecho, se deben realizar los siguientes cambios en los archivos de configuración, cambiando los puertos 80 por 8081.

Los siguientes comandos son los siguientes:

    sudo vi /etc/apache2/ports.conf

    sudo vi /etc/apache2/sites-enabled/000-default.conf

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%205.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%206.png)
En mi caso, en los comandos, en vez de usar vi; usé nano para editarlos.
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%207.png)

Reiniciamos los servicios con los comandos:

    sudo systemctl restart apache2
    sudo service apache2 restart

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%208.png)

Y ajustamos la configuración de Firewall con el comando:

    sudo ufw app list

Con el consiguiente mensaje:

    Available applications:
    Apache
    Apache Full
    Apache Secure
    OpenSSH

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%209.png)

Ahora, usaremos el perfil Apache que no será necesario usar la conexión cifrada con el comando:

    sudo ufw allow 'Apache'

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%209.png)

Verificando los perfiles activos y, además, verificando si Apache se está ejecutando correctamente, con los siguientes comandos:

    sudo ufw status

Con el siguiente resultado de los perfiles:
    Status: active
    To             Action         From
    --             ------         ----
    Apache         ALLOW          Anywhere
    Apache (v6)    ALLOW          Anywhere (v6)

Si no está funcionando a la primera (como en mi caso), lo que haremos será ejecutar el comando para activarlo:

    sudo ufw enable



Y la verificación de Apache funcionando:

    sudo systemctl status apache2

    Con su correspondiente resultado:
    ● apache2.service - The Apache HTTP Server
    Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
    Active: active (running) since Tue 2021-10-05 16:11:23 WEST; 3min 2s ago
    Docs: https://httpd.apache.org/docs/2.4/
    Process: 3081 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
    Main PID: 3100 (apache2)
    Tasks: 55 (limit: 4681)
    Memory: 7.2M
    CGroup: /system.slice/apache2.service
            ├─3100 /usr/sbin/apache2 -k start
            ├─3101 /usr/sbin/apache2 -k start
            └─3102 /usr/sbin/apache2 -k start

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%2010.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%2011.png)
![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%2012.png)

 ### 3. ACCESO

 Una vez realizado todo este segundo paso, procedemos a confirmar si el servicio se está ejecutando correctamente

    http://tu_ip:8081 o localhost:8081

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%205%20-%20Instalaci%C3%B3n%20de%20Apache%20en%20Linux/Apache%2013.png)
