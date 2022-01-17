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

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%201.png)

Una vez agregado, el sistema nos devolverá OK. Y ahora anexamos la dirección del repositorio de paquetes de Debian a sources.list del servidor, con el comando:

    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%202.png)

Ejecutamos el apt update para que utilice el nuevo repositorio, con el comando:

    sudo apt update

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%203.png)

Y para finalizar, instalamos Jenkins y sus dependencias correspondientes, con el comando:

    sudo apt install jenkins

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%204.png)

 ### 2. INICIAR JENKINS

Una vez instalado Jenkins, iniciamos el servicio con el comando:

    sudo systemctl start jenkins

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%205.png)

Verificamos su estado con el comando:

    sudo systemctl status jenkins

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%206.png)

Si funciona todo a la perfección, procedemos a ajustar ahora el firewall.

 ### 3. ABRIR EL FIREWALL

Para configurar el firewall, ejecutamos el comando:

    sudo ufw allow 8080

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%207.png)

Si el firewall lo tenemos desactivado, activamos Open SSH con el comando:

    sudo ufw allow OpenSSH

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%208.png)

    sudo ufw enable

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%209.png)

Comprobamos el estado de ufw:

    sudo ufw status

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2010.png)

Y si tenemos configurado el firewall de Jenkins, procedemos a la configuración de la misma.

 ### 4. CONFIGURAR JENKINS

Para hacer la configuración del servicio Jenkins, tendremos que crear nuestro propio dominio que, en este caso, será www.jorgeev.com:8080 (el puerto predeterminado que le pusimos pasos atrás).

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2012.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2013.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2014.png)

Una vez realizado los procesos para que nuestro dominio esté funcionando correctamente, deberíamos ver la pantall Unlock Jenkins, que muestra la ubicación de la contraseña inicial para que podamos seguir adelante:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2015.png)

En una terminal, utilizamos dicho comando para que se muestre la contraseña correspondiente:

    sudo cat /var/lib/jenkins/secrets/initialAdminPassword

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2016.png)

La contraseña es alfanumérica de 32 caracteres, y la pegamos en el campo de Administrator password y clickeamos en Continue.

Y en la siguiente pantalla, hacemos click en Install suggested plugins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2017.png)

Una vez instalado, creamos nuestro usuario. Y una vez creado, Jenkins nos dirá que está preparado.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2018.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2019.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2020.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2025%20-%20Instalaci%C3%B3n%20y%20configuraci%C3%B3n%20de%20Jenkins%20en%20Linux/Jenkins%2021.png)
