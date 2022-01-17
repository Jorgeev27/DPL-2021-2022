# Tarea 25 - Instalación y configuración de Jenkins en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalación de Jenkins
 - Iniciar Jenkins
 - Abrir el Firewall
 - Configurar Jenkins

 ### 1. INSTALACIÓN DE JENKINS

Primero, agregamos la clave del repositorio de Jenkins a nuestro sistema, con el comando:

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add

Una vez agregado, el sistema nos devolverá OK. Y ahora anexamos la dirección del repositorio de paquetes de Debian a sources.list del servidor, con el comando:

    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

Ejecutamos el apt update para que utilice el nuevo repositorio, con el comando:

    sudo apt update

Y para finalizar, instalamos Jenkins y sus dependencias correspondientes, con el comando:

    sudo apt install jenkins

 ### 2. INICIAR JENKINS

Una vez instalado Jenkins, iniciamos el servicio con el comando:

    sudo systemctl start jenkins

Verificamos su estado con el comando:

    sudo systemctl status jenkins

Si funciona todo a la perfección, procedemos a ajustar ahora el firewall.

 ### 3. ABRIR EL FIREWALL

Para configurar el firewall, ejecutamos el comando:

    sudo ufw allow 8080

Si el firewall lo tenemos desactivado, activamos Open SSH con el comando:

    sudo ufw allow OpenSSH
    sudo ufw enable

Comprobamos el estado de ufw:

    sudo ufw status

Y si tenemos configurado el firewall de Jenkins, procedemos a la configuración de la misma.

 ### 4. CONFIGURAR JENKINS

Para hacer la configuración del servicio Jenkins, tendremos que crear nuestro propio dominio que, en este caso, será www.jorgeev.com:8080 (el puerto predeterminado que le pusimos pasos atrás).

Una vez realizado los procesos para que nuestro dominio esté funcionando correctamente, deberíamos ver la pantall Unlock Jenkins, que muestra la ubicación de la contraseña inicial para que podamos seguir adelante:

En una terminal, utilizamos dicho comando para que se muestre la contraseña correspondiente:

    sudo cat /var/lib/jenkins/secrets/initialAdminPassword

La contraseña es alfanumérica de 32 caracteres, y la pegamos en el campo de Administrator password y clickeamos en Continue.

Y en la siguiente pantalla, hacemos click en Install suggested plugins.

Una vez instalado, creamos nuestro usuario. Y una vez creado, Jenkins nos dirá que está preparado.
