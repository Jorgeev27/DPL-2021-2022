# Tarea 3 - Ejemplos de GIT: Manipulación Avanzada de repositorios en GIT
  
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
 
 Para poder realizar los ejemplos, se debe haber hecho anteriormente los ejercicios del historial de cambios o hacer un clon del repositorio remoto https://github.com/jpexposito/libro a través de los siguientes comandos:
 
    git clone https://github.com/jpexposito/libro.git
    cd libro
 
 ![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%201.png)
 
 ### 1. HISTORIAL DE CAMBIOS DEL REPOSITORIO Y FICHERO CAPÍTULO 1

Habrá que mostrar el historial de los cambios del repositorio y crear la carpeta capítulos. Dentro de ella, creamos el fichero capitulo1.txt con el siguiente texto (Git es un sistema de control de versiones ideado por Linus Torvalds.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Añadido capítulo 1.”. Y una vez realizado todo este proceso, volvemos a mostrar el historial de los cambios del repositorio.

Estos son los comandos que hay que utilizar para ello:

    git log

    mkdir capitulos

    cat > capitulos/capitulo1.txt

    Git es un sistema de control de versiones ideado por Linus Torvalds.
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Añadido capítulo 1."

    git log
    
![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%202.png)
  
  ### 2. FICHERO CAPÍTULO 2
  
Creamos un fichero llamado capitulo2.txt en la carpeta capitulos con el siguiente texto (El flujo de trabajo básico con Git consiste en: 1- Hacer cambios en el repositorio. 2- Añadir los cambios a la zona de intercambio temporal. 3- Hacer un commit de los cambios.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Añadido capítulo 2.”. Y una vez realizado todo, mostramos las diferencias entre la última versión y las dos versiones anteriores que hemos creado.

Estos son los comandos que hay que utilizar para ello:

    cat > capitulos/capitulo2.txt

    El flujo de trabajo básico con Git consiste en:
    1- Hacer cambios en el repositorio.
    2- Añadir los cambios a la zona de intercambio temporal.
    3- Hacer un commit de los cambios.
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Añadido capítulo 2."

    git diff HEAD~2..HEAD


![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%203.png)

 ### 3. FICHERO CAPÍTULO 3
 
Creamos un fichero llamado capitulo3.txt en la carpeta capítulos con el siguiente texto (Git permite la creación de ramas lo que permite tener distintas versiones del mismo proyecto y trabajar de manera simultánea en ellas.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Añadido capítulo 3.”. Y una vez realizado todo, mostramos diferencias entre la primera y la última versión del repositorio.

Estos son los comandos que hay que utilizar para ello:

    cat > capitulos/capitulo3.txt

    Git permite la creación de ramas lo que permite tener distintas versiones del mismo proyecto y trabajar de manera simultanea en ellas.
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Añadido capítulo 3."

    git log

    git diff <codigo hash de la primera version>..HEAD

![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%204.png)
   
 ### 4. FICHERO ÍNDICE
 
Creamos un fichero llamado indice.txt en la carpeta capitulos con el siguiente texto (Indice de los capítulos, con conceptos avanzados de git.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Indice de los capítulos, con conceptos avanzados de git.”. Y una vez realizado todo, mostramos quién ha hecho los cambios sobre el propio fichero indice.txt.

Estos son los comandos que hay que utilizar para ello:

    cat > indice.txt

    Indice de los cápitulos, con conceptos avanzados de git
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Se crea el indice."

    echo "Indice de los capítulos, con conceptos avanzados de git" >> indice.txt

    git add .

    git commit -m "Añadido el índice ."

    git annotate indice.txt


![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%205.png)

 ### 5. RAMA BIBLIOGRAFÍA
 
Creamos una nueva rama llamada bibliografía y mostramos las ramas del repositorio. Para ello, utilizaremos el siguiente comando:

    git branch bibliografia

    git branch -av
    
![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%207.png)

 ### 6. FICHERO CAPÍTULO 4
 
Creamos un fichero llamado capitulo4.txt en la carpeta capítulos con el siguiente texto (En este capítulo veremos cómo usar GitHub para alojar repositorios en remoto.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Añadido capítulo 4.”. Y una vez realizado todo, mostramos el historial del repositorio, incluyendo todas las ramas realizadas anteriormente.

Estos son los comandos que hay que utilizar para ello:

    cat > capitulos/capitulo4.txt

    En este capítulo veremos cómo usar GitHub para alojar repositorios en remoto.
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Añadido capítulo 4."

    git log --graph --all --oneline

![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%208.png)

 ### 7. FICHERO BIBLIOGRAFÍA
 
Cambiamos a la rama bibliografia y creamos un fichero llamado bibliografia.txt con el siguiente texto (Chacon, S. and Straub, B. Pro Git. Apress.). Añadimos los cambios a una zona temporal, hacemos un commit de los cambios con el siguiente mensaje “Añadida primera referencia bibliográfica.”. Y una vez realizado todo, mostramos el historial del repositorio, incluyendo todas las ramas realizadas anteriormente.

Estos son los comandos que hay que utilizar para ello:

    git checkout bibliografia

    cat > bibliografia.txt

    Chacon, S. and Straub, B. Pro Git. Apress. 
    Ctrl+D (guardamos el fichero txt)

    git add .

    git commit -m "Añadida primera referencia bibliográfica."

    git log --graph --all --oneline

![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%208.png)
 
 ### 8. FUSIÓN RAMA BIBLIOGRÁFICA CON RAMA MAIN
 
Fusionamos la rama bibliográfica con la rama main, mostrando el historial del repositorio, incluyendo todas las ramas realizadas anteriormente; eliminamos la rama bibliográfica y mostramos de nuevo el historial del repositorio, incluyendo todas las ramas realizadas anteriormente.

Estos son los comandos que hay que utilizar para ello:

    git checkout main

    git merge bibliografia

    git log --graph --all --oneline

    git branch -d bibliografia

    git log --graph --all --oneline
 
 ![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%209.png)
 
 ### 9. RAMA BIBLIOGRÁFICA, FICHERO BIBLIOGRAFÍA, RAMA MAIN
 
Creamos la rama bibliográfica, cambiamos a la rama bibliografía, y cambiamos el fichero bibliografia.txt para que contenga el siguiente texto (Scott Chacon and Ben Straub. Pro Git. Apress. Ryan Hodson. Ry’s Git Tutorial. Smashwords (2014)); cambiamos a la rama main y cambiamos el fichero bibliografia.txt para que contenga el siguiente texto (Chacon, S. and Straub, B. Pro Git. Apress. Loeliger, J. and McCullough, M. Version control with Git. O’Reilly.)

Añadimos los cambios a una zona temporal, hacemos un commit con el mensaje “Añadida nueva referencia bibliográfica.”; fusionamos la rama bibliográfica con la rama main y resolvemos el conflicto dejando el fichero bibliografia.txt con el siguiente texto (Chacon, S. and Straub, B. Pro Git. Apress. Loeliger, J. and McCullough, M. Version control with Git. O’Reilly.)

Añadimos los cambios a la zona temporal y hacemos un commit con el mensaje “Resuelto conflicto de bibliografía.”, y por último, mostramos el historial del repositorio incluyendo todas las ramas realizadas anteriormente.+

Todos estos procesos se hacen a través de los siguientes comandos:

    git branch bibliografia

    git checkout bibliografia

    cat > bibliografia.txt

    Scott Chacon and Ben Straub. Pro Git. Apress.
    Ryan Hodson. Ry's Git Tutorial. Smashwords (2014)
    Ctrl+D (guardamos el fichero txt)

    git commit -a -m "Añadida nueva referencia bibliográfica."

    git checkout main

    cat > bibliografia.txt

    Chacon, S. and Straub, B. Pro Git. Apress.
    Loeliger, J. and McCullough, M. Version control with Git. O'Reilly.
    Ctrl+D (guardamos el fichero txt)

    git commit -a -m "Añadida nueva referencia bibliográfica."

    git merge bibliografia

    git nano bibliografia

    #Hacer los cambios indicados en el fichero

    git commit -a -m "Solucionado conflicto bibliografía."

    git log --graph --all --oneline


Hay más opciones para poder configurar, pero estas 2 son las opciones más comunes.

![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%2010.png)


Aquí me daba un error porque, al parecer, no me cogía el comando “nano” de GIT. Entonces, ese paso del comando (git nano bibliografia), me lo tuve que saltar tras varios intentos y alguna búsqueda en internet pero sin acierto.
![](https://github.com/Jorgeev27/DPL/blob/main/img/Tarea%201%20-%20Instalaci%C3%B3n%20de%20Git%20en%20linux/Git%2011.png)

