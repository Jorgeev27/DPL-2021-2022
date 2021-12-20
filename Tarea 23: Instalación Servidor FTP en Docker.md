# Tarea 23: Instalación Servidor FTP en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalación de SFTP
 - Trabajando con la Imagen atmoz
 - Verificar la Imagen
 - Configurar el Directorio /home en la Máquina Host
 - SFTP Multiusuario

 ### 1. INSTALACIÓN DE SFTP

Realizamos la búsqueda de imágenes creadas y contrastadas en https://hub.docker.com/search?q=sftp&type=image. Y vemos que existen diferentes imágenes creadas para instalar SFTP.

Y podemos realizar la búsqueda de la imagen a través del comando:

    sudo docker search sftp

Y con la siguiente salida en el comando:

    NAME                      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
    atmoz/sftp                Easy to use SFTP server                         402                  [OK]
    drakkan/sftpgo            Official build of SFTPGo. SFTP/FTP/WebDAV se…   20                   
    writl/sftp                SFTP-Server with changeable uid and gid         14                   [OK]
    emberstack/sftp           SFTP (SSH File Transfer Protocol) server usi…   12                   
    turgon37/sftp-ldap        Docker image running a SFTP server with a LD…   5                    [OK]
    netresearch/sftp          Easy to use SFTP (SSH File Transfer Protocol…   3                    [OK]
    markusmcnugen/sftp        Fork of atmoz SFTP docker container built wi…   3                    [OK]
    amimof/sftp               A fast and secure SFTP server that runs in a…   3                    [OK]
    asavartzeth/sftp          A dockerized sftp server, using the openssh …   2                    [OK]
    hectormolinero/sftp       A Docker image with an OpenSSH server config…   2                    
    chessracer/sftp-s3fs      SFTP with built-in s3fs - Aws s3 mounted to …   2                    [OK]
    corilus/sftp              Securely share your files, with full rsyslog…   1                    
    yakworks/sftp             sftp with fail2ban and kubernetes support       1                    
    noc0lour/sftp             simple sftp/scp/rsync container with rssh       0                    [OK]
    proatria/sftpplus-trial   Trial version for SFTPPlus.                     0                    
    ahatting/sftp             Source project: hub.docker.com/r/atmoz/sftp/    0                    
    famartinez76/sftp2525     Modified version of the atmoz/sftp image but…   0                    
    ez123/sftp                sftp                                            0                    [OK]
    famartinez76/sftp2222     Modified version of the atmoz/sftp image but…   0                    
    cvitkoilm/sftp            Fork of atmoz/sftp that will work on Azure w…   0                    [OK]
    rabii17/sftp                                                              0                    
    rsmdockers/sftp                                                           0                    
    mauwii/sftp                                                               0                    
    dazoe/sftp                simple sftp docker                              0                    
    triskellesolutions/sftp                                                   0           


 ### 2. TRABAJANDO CON LA IMAGEN ATMOZ

Utilizamos la imagen desarrollada por atmoz sobre sftp. Y realizamos los siguientes pasos:

    docker run --name mysftp -p 2294:22 -d atmoz/sftp admin:admin:::upload

donde:

- name: Nombre del contenedor mysftp.
- admin:admin:::upload: foo es el nombre de usuario, pass contraseña, upload es el archivo cargado donde se guardará en /home/foo/upload en el contenedor.
- -p 22:22: asigna el puerto 22 del host al puerto 22 del contenedor, y que el puerto 22 del host de ubicación se reenviará al puerto 22 del contenedor.
- -d atmoz/sftp: la imagen atmoz/sftp en el centro de acoplamiento para crear el contenedor.


 ### 3. VERIFICAR LA IMAGEN

Para verificar la descarga de la imagen, lanzamos el comando:

    sudo docker ps | grep sftp

Y obtenemos el siguiente resultado:

    ffa078007f2e   atmoz/sftp   "/entrypoint admin:a…"   4 minutes ago   Up 4 minutes   0.0.0.0:2294->22/tcp   mysftp

Se puede realizar la prueba de acceso al servidor FTP. Para ello, lanzamos los comandos:

    sudo docker ps

Y obtenemos:

    CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                  NAMES
    ffa078007f2e   atmoz/sftp   "/entrypoint admin:a…"   13 minutes ago   Up 13 minutes   0.0.0.0:2294->22/tcp   mysftp

    docker inspect ffa078007f2e | grep "IPAddress"
            "SecondaryIPAddresses": null,
             "IPAddress": "172.17.0.2",
                     "IPAddress": "172.17.0.2",


 ### 4. CONFIGURAR EL DIRECTORIO /HOME EN LA MÁQUINA HOST

Para realizar la configuración del directorio /home de SFTP, ejecutamos el comando:

    sudo docker run --name mysftp2 -v /host/upload:/home/admin/upload --privileged=true -p 2295:22 -d atmoz/sftp admin:admin:1001

donde:

- -v /host/upload:/home/admin/upload: El frente de los puntos es el directorio del host, y la parte posterior se monta en el directorio del contenedor, si el directorio local /host/upload no existe, se creará automáticamente.
- --privileged=true: Se agregan privilegios de seguridad de selinux de linux al contenedor.
- --name mysftp2: El nombre se cambiará debido a que no se puede repetir, el puerto sí se puede repetir aunque el contenedor no se va a iniciar.


 ### 5. SFTP MULTIUSUARIO

Si se desea configurar varios usuarios sftp, habrá que:

- Crear usuarios en el contenedor y asignamos permisos.
- Escribir archivos de usuario en el host y los montamos en el contenedor.

El primer método será utilizar directamente el ejemplo anterior.
El segundo método es implementarlo, y para ello, utilizamos el comando:

    sudo docker run --name mysftp3 -v /host/users.conf:/etc/sftp/users.conf:ro -v /home/sftp:/home --privileged=true -p 2296:22 -d atmoz/sftp

donde:

- -v /host/users.conf:/etc/sftp/users.conf:ro: Se mapea el /host/users.conf local al /etc/sftp/users.conf del contenedor, y es de sólo lectura del contenedor.
- -v /home/sftp:/home: Se asigna el directorio local /home/sftp al contenedor /home para almacenar los archivos cargados.

Y no habrá que olvidar crear el archivo /host/users.conf en el directorio local.

    sudo nano /host/users.conf

Y el archivo users.conf:

    xiaoming:123:1001:100
    goudan:abc:1002:100
    erzhu:xyz:1003:100

donde 
- usuario:contraseña:uid:gid - Nombre de usuario:Contraseña:ID de usuario: ID de grupo.
