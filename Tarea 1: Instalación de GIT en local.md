  # Tarea 1: Instalación de Git en linux
  
  ## Jorge Escobar Viñuales
  
  ## Indice:
 - Instalando GIT
 - Actualizar los paquetes
 - Directorio temporal
 - Descomprimir el archivo tarball
 - Directorio de GIT
 - Sustitución shell
 - Configuración para realizar la instalación (paso 1)
 - GIT config
 - Archivo de configuración GIT
 
 ### 1. INSTALANDO GIT

Instalación de GIT - para buscar en tu sistema si GIT está instalado, se utilizará el siguiente comando:

	git --version

Y si viene instalado te aparece la versión correspondiente. En mi caso, al tener una máquina virtual Ubuntu 18.04, no tenía instalado GIT y tuve que instalar GIT con el siguiente comando: 

	sudo apt install git

![](https://github.com/Jorgeev27/sadas/blob/main/DPL/IMG/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%201.png)
![](https://github.com/Jorgeev27/sadas/blob/main/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%202.png)
  
  ### 2. ACTUALIZAR LOS PAQUETES
  
Una vez instalado GIT, se debe actualizar los paquetes de estos, para ello utilizaremos el siguiente comando:

	sudo apt update 

	sudo apt install libz-dev libssl-dev libcurl4-gnutls-dev libexpat1-dev gettext cmake gcc

![](https://github.com/Jorgeev27/sadas/blob/main/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%203.png)

 ### 3. DIRECTORIO TEMPORAL
 
El siguiente paso sería crear un directorio temporal:

	mkdir tmp

	cd /tmp

Una vez realizada la carpeta temporal, colocaremos aquí el tarball de GIT. Para ello, iremos a la página del proyecto de GIT y cogeremos la versión más reciente para tenerlo a nuestra disposición, con el siguiente comando:

	curl -o git.tar.gz https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.29.3.tar.gz

En mi caso, al no tener curl instalado, lo tuve que instalar con el comando:

	sudo apt install curl

Y ya al instalar curl, procedí a instalar la versión más reciente.

![](https://github.com/Jorgeev27/sadas/blob/main/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%204.png)
   
 ### 4. DESCOMPRIMIR EL ARCHIVO TARBALL
 
  Descomprimir el archivo de tarball:

	tar -zxf git.tar.gz

![](https://github.com/Jorgeev27/sadas/blob/main/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%205.png)

 ### 5. DIRECTORIO DE GIT
 
Ahora, nos vamos al nuevo directorio de GIT:

	cd git-*

Y crear el paquete e instalarlo con estos 2 comandos:

	make prefix=/usr/local all

	sudo make prefix=/usr/local install

![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

 ### 6. SUSTITUCIÓN SHELL
 
Se hace la sustitución de shell para utilizar la versión de GIT que acabamos de instalar anteriormente:

	exec bash

Y una vez completado todo este proceso, lo siguiente y último, es comprobar la versión de GIT se ha realizado con éxito:

	git --version

Si GIT está instalado y funcionando correctamente, ahora se procede a su configuración.

![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
 
 ## CONFIGURACION DE GIT
 ### 7. CONFIGURACIÓN PARA REALIZAR LA INSTALACIÓN (PASO 1)
 
Para realizar la configuración, hay que seguir los pasos comentados anteriormente de la instalación de GIT.
 
 ### 8. GIT CONFIG
 
Empezamos con el comando git config, el cual te permite poner nuestro nombre, correo electrónico para que confirme cada información que procesamos en ese instante:

	git config --global user.name "Your Name"

	git config --global user.email "youremail@domain.com"

Y para ver todos los elementos de la configuración con:

	git config --list
 
 ![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
 
 ### 9. ARCHIVO CONFIGURACIÓN GIT
 
Esta información se almacena en el archivo de configuración de GIT. Hay que editarlo manualmente con cualquier editor de texto:

	nano ~/.gitconfig

Hay más opciones para poder configurar, pero estas 2 son las opciones más comunes.

![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
