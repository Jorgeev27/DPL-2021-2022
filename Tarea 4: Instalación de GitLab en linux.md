# Tarea 4: Instalación de GitLab en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Actualización de los repositorios
 - Instalación de paquetes adicionales
 - Instalación de GitLab
 - Acceso

 Para poder realizar la actividad, se necesitará una máquina Linux.

 ### 1. ACTUALIZACIÓN DE LOS REPOSITORIOS

Antes de comenzar cualquier instalación de cualquier programa, se recomienda actualizar el repositorio del sistema operativo. De este modo, la intalación de GitLab en cualquier Ubuntu es siempre segura y actualizada

Para ello, utilizaremos estos dos comandos:

    sudo apt update

    sudo apt upgrade

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%203%20-%20Ejemplos%20en%20GIT%20Manipulaci%C3%B3n%20Avanzada%20de%20repositorios%20en%20Git/Manipulaci%C3%B3n%20GIT%202.png)

  ### 2. INSTALACIÓN DE PAQUETES ADICIONALES

Además, instalar paquetes necesarios para instalar GitLab en los sistemas Ubuntu.

Para ello, utilizaremos este comando:

    sudo apt install -y vim curl ca-certificates apt-transport-https


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%203%20-%20Ejemplos%20en%20GIT%20Manipulaci%C3%B3n%20Avanzada%20de%20repositorios%20en%20Git/Manipulaci%C3%B3n%20GIT%203.png)

 ### 3. INTALACIÓN DE GITLAB

El equipo de GitLab nos proporciona un script de shell para configurar el repositorio APT en su sistema, así como para instalar algunas dependencias necesarias.

Estos son los comandos que hay que utilizar para ello:

    curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash

    sudo apt install gitlab-ce

Para terminar con la instalación, se debe de ejecutar el siguiente comando para configurar el gitlab:

    sudo gitlab-ctl reconfigure


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%203%20-%20Ejemplos%20en%20GIT%20Manipulaci%C3%B3n%20Avanzada%20de%20repositorios%20en%20Git/Manipulaci%C3%B3n%20GIT%204.png)

 ### 4. ACCESO

Una vez hecho la instalación, se procederá a acceder a través de un navegador; poniendo localhost o la dirección ip de nuestro ordenador para acceder al servidor

    localhost


![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%203%20-%20Ejemplos%20en%20GIT%20Manipulaci%C3%B3n%20Avanzada%20de%20repositorios%20en%20Git/Manipulaci%C3%B3n%20GIT%2019.png)
