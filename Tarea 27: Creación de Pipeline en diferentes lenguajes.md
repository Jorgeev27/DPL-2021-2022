# Tarea 27: Creación de Pipeline en diferentes lenguajes

  ## Jorge Escobar Viñuales

  ## Indice:
 - Creación de una Nueva Tarea Jenkins
 - Pipeline JAVA
 - Pipeline NodeJS
 - Pipeline Ruby
 - Pipeline Python
 - Pipeline PHP
 - Pipeline GO

 ### 1. CREACIÓN DE UNA NUEVA TAREA JENKINS

En el panel de control de Jenkins, tenemos la opción de “Nueva tarea”.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%201.png)

 ### 2. PIPELINE JAVA

Una vez seleccionada la opción de “Nueva tarea”, le ponemos el nombre de Jenkins JAVA y elegimos el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%202.png)

El siguiente paso, será poner el script de JAVA para que lo ejecute Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%203.png)

Ejecutamos el Pipeline JAVA y se nos mostrará el siguiente error:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%204.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%205.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%206.png)

Para que este error quede solucionado, haremos estos 3 pasos:

  - Vamos al apartado “Administrar plugins” de nuestro panel de control e instalamos los plugins Docker y Docker Pipeline. Y una vez instalado, reiniciamos el servicio Jenkins.
  - Añadimos permisos de usermod, con el comando: sudo usermod -a -G docker jenkins.
  - Y añadimos el usuario jenkins en /etc/sudoers

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%207.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%208.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%209.png)

Y una vez realizado estos 3 pasos, Pipeline JAVA funciona a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2010.png)

 ### 3. PIPELINE NODEJS

Haremos lo mismo que en los pasos anteriores: creación de una “Nueva tarea” y el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2011.png)

Inserción del script que va a ejecutar Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2012.png)

Ejecutamos la tarea y funcionará a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2013.png)

 ### 4. PIPELINE RUBY

Haremos lo mismo que en los pasos anteriores: creación de una “Nueva tarea” y el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2014.png)

Inserción del script que va a ejecutar Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2015.png)

Ejecutamos la tarea y funcionará a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2016.png)

 ### 5. PIPELINE PYTHON

Haremos lo mismo que en los pasos anteriores: creación de una “Nueva tarea” y el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2017.png)

Inserción del script que va a ejecutar Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2018.png)

Ejecutamos la tarea y funcionará a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2019.png)

 ### 6. PIPELINE PHP

Haremos lo mismo que en los pasos anteriores: creación de una “Nueva tarea” y el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2020.png)

Inserción del script que va a ejecutar Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2021.png)

Ejecutamos la tarea y funcionará a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2022.png)

 ### 7. PIPELINE GO

Haremos lo mismo que en los pasos anteriores: creación de una “Nueva tarea” y el tipo Jenkins.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2023.png)

Inserción del script que va a ejecutar Pipeline.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2024.png)

Ejecutamos la tarea y funcionará a la perfección.

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2027%20-%20Creaci%C3%B3n%20de%20Pipeline%20en%20diferentes%20lenguajes/Pipeline%20Jenkins%2025.png)
