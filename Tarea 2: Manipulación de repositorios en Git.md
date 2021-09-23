# Tarea 2: Instalación de Git en linux
  
  ## Jorge Escobar Viñuales
  
  ## Indice:
 - Configurar GIT
 - Crear repositorio
 - Estado del repositorio
 - Configuración fichero indice.txt
 - Commit de los cambios
 - Modificación fichero indice.txt
 - Historial

Para realizar esta tarea se necesita la máquina virtual de Linux y la tarea anterior realizada (instalación y configuración de git).

  ### 1. CONFIGURAR GIT
  
Configurar el GIT con tu nombre, correo electrónico y activar el coloreado de salida:

    git config --global user.name "Your-Full-Name"
    git config --global user.email "your-email-address"
    git config --global color.ui auto
    git config --list
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

  ### 2. CREAR REPOSITORIO
Crea un repositorio nuevo con el nombre de DPL y mostrar el contenido de la misma:

    mkdir dpl
    cd dpl
    git init
    ls -la
    
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)
 
  ### 3. ESTADO DEL REPOSITORIO
  El siguiente paso es comprobar el estado del repositorio
  
  ### 4. CONFIGURACIÓN FICHERO INDICE.TXT
  
Después de ello, creas un fichero llamado indice.txt con el siguiente contenido: 

  - Capítulo 1: Instalación de GIT por el alumno Jorge Escobar Viñuales
  - Capítulo 2: Flujo de trabajo básico por el alumno Jorge Escobar Viñuales

Comprobamos el estado del repositorio de nuevo, añadimos el fichero a una zona temporal y comprobamos el estado del repositorio.

  
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

  ### 5. COMMIT DE LOS CAMBIOS
Ahora, realizas un commit de los cambios con el mensaje “Añadido índice de la asignatura DPL.” y ver el estado del repositorio.

    git commit -m "Añadido índice de la asignatura DPL."
    git status
  
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

  ### 6. MODIFICACIÓN FICHERO INDICE.TXT
Con la modificación de ficheros, cambiamos el fichero indice.txt añadiendo los capítulos 3 y 4:

  - Capítulo 1: Instalación de GIT por el alumno Jorge Escobar Viñuales
  - Capítulo 2: Flujo de trabajo básico por el alumno Jorge Escobar Viñuales
  - Capítulo 3: Gestión de ramas por el alumno Jorge Escobar Viñuales
  - Capítulo 4: Repositorios remotos por el alumno Jorge Escobar Viñuales

Mostramos los cambios con respecto a la última versión del repositorio y hacemos un commit de los cambios actuales:

    cat > indice.txt
    Capítulo 1: Instalación de Git por el alumno XXX _(donde XXX es el nombre del alumno)_
    Capítulo 2: Flujo de trabajo básico
    Capítulo 3: Gestión de ramas
    Capítulo 4: Repositorios remotos
    Ctrl+D
    git diff
    git add indice.txt
    git commit -m "Añadido los capitulos 3"

  
![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

  ### 7. HISTORIAL
  Para ver el historial, mostramos los cambios de la última versión del repositorio; cambiando el mensaje del último commit por “Añadido el capítulo sobre gestión de ramas de índice”. Después de eso, volvemos a mostrar los últimos cambios del repositorio:

    git show
    git commit --amend -m "Añadido el capitulo sobre gestión de ramas al índice."
    git show
  
  ![](https://github.com/Jorgeev27/sadas/blob/765a0e440006ce373ad3f96b63a8c681b4ca0f87/Sin%20t%C3%ADtulo.jpg)

