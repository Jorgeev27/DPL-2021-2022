# Tarea 22: Instalación Servidor FTP en Ubuntu

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalación de FTP
 - Verificación del Servicio FTP en Ubuntu
 - Configuración del Servidor FTP
 - Instalación de un Cliente o Utilización de un Cliente

 ### 1. INSTALACIÓN DE FTP

Habrá que hacer una actualización de los repositorios con el comando:

    sudo apt update

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%201.png)

Y después haremos la instalación del paquete vsftpd con el comando:

    sudo apt install -y vsftpd

Obteniendo el siguiente mensaje de que se ha instalado correctamente:

    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    The following additional packages will be installed:
      cron libcap2 libpopt0 libwrap0 logrotate netbase ssl-cert
    Suggested packages:
      anacron checksecurity default-mta | mail-transport-agent bsd-mailx | mailx
      openssl-blacklist
    The following NEW packages will be installed:
    …


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%202.png)

Si el firewall está activado, habrá que permitir el acceso a los puertos del servicio FTP, como el puerto de comandos:

    sudo ufw allow ftp


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%203.png)

Y el de los puertos de datos, para que estén en modo activo:

    sudo ufw allow ftp-data

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%204.png)

 ### 2. VERIFICACIÓN DEL SERVICIO FTP EN UBUNTU

Para hacer una prueba del servicio, lo haremos desde otra máquina (o desde nuestro propio navegador) usando:

    ftp://IP


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%205.png)


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%206.png)

Al hacer ftp://IP, me salta este fallo de Firefox que impide acceder.


 ### 3. CONFIGURACIÓN DEL SERVICIO FTP

Para configurar el servidor FTP vsFTPd, trabajamos sobre su archivo principal vsftpd.conf, que se encuentra en la ruta /etc/.


 ### 4. INSTALACIÓN DE UN CLIENTE O UTILIZACIÓN DE UN CLIENTE

Para realizar el acceso y configuración hay que disponer o instalar el cliente ftp. Para ello también, debemos disponer el servidor de filezilla, con el comando:

    sudo apt install filezilla


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%207.png)

Para ello, accedemos al servidor FTP desde la línea de comandos:

    ftp IP

Y activamos el modo pasivo, que en este caso nos viene por defecto activado:


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%208.png)

Configuramos el archivo vsftpd.conf:

    sudo nano /etc/vsftpd.conf

Y añadimos las directivas al final del archivo de configuración:

    pasv_enable=YES
    pasv_min_port=30000
    pasv_max_port=30050

Y una vez realizado estos cambios, recargamos la configuración del servicio con el comando:

    sudo systemctl reload vsftpd


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%209.png)


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2010.png)

Si el servidor tiene activado el Firewall UFW, permitimos el acceso el rango de los puertos que acabamos de añadir en el archivo de configuración:

    sudo ufw allow 30000:30050/tcp


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2011.png)

Y desde el archivo de configuración, realizamos la verificación del acceso al cliente filezilla. Si queremos usuarios anónimos desactivamos el acceso a usuarios del sistema:

    ...
    local_enable=YES
    ...

Y que los usuarios locales puedan escribir en sus directorios:

    ...
    # Uncomment this to enable any form of FTP write command.
    #write_enable=YES
    ...

En mi caso, no desactivé el acceso a los usuarios locales.

Ahora, descomentamos la directiva write_enable para que los usuarios puedan crear o eliminar archivos y directorios:

    ...
    # Uncomment this to enable any form of FTP write command.
    write_enable=YES
    ...


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2012.png)

Y activamos el enjaulado de los usuarios, para que los usuarios locales naveguen por todo el sistema de archivos de Ubuntu:

    chroot_local_user=YES

Y para evitar eliminar archivos o directorios, cambiamos los permisos de los directorios o añadimos la directiva allow_writeable_chroot:

    chroot_local_user=YES
    allow_writeable_chroot=YES


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2013.png)

Y recargamos el servicio:

    sudo systemctl reload vsftpd


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2014.png)

Y Filezilla funcionando:


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2022%20-%20Instalaci%C3%B3n%20de%20FTP%20en%20Linux/FTP%2015.png)
