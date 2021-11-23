# Tarea 20: Balanceo de Carga en Apache

  ## Jorge Escobar Viñuales

  ## Indice:
 - Activación de los módulos necesarios de Apache
 - Configuración de Apache para trabajar como balanceador de cargas para el tráfico HTTP
 - Funcionamiento

 ### 1. ACTIVACIÓN DE LOS MÓDULOS NECESARIOS DE APACHE

Vamos a activar la activación de los nodos necesarios en Apache. Los comandos para activar son los siguientes:

    a2enmod proxy
    a2enmod proxy_http
    a2enmod proxy_ajp
    a2enmod rewrite
    a2enmod deflate
    a2enmod headers
    a2enmod proxy_balancer
    a2enmod proxy_connect
    a2enmod proxy_html
    a2enmod lbmethod_byrequests

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%201.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%202.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%203.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%204.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%205.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%206.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%207.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%208.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%209.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2010.png)

Si hay que desactivar un módulo, deberemos de utilizar:

    a2dismod proxy_ajp

Una vez realizada la activación de los módulos necesarios, debemos realizar un reinicio del servicio de Apache:

    systemctl restart apache2

 ### 2. CONFIGURACIÓN DE APACHE PARA TRABAJAR COMO BALANCEADOR DE CARGAS PARA EL TRÁFICO HTTP

Editamos el archivo 000-default.conf que está en el directorio /etc/apache2/sites-available:

    sudo nano /etc/apache2/sites-available/000-default.conf

Y añadimos las directivas de Proxy y ProxyPass dentro del VirtualHost:

    <VirtualHost *:80>
      # Dejamos la configuración del VirtualHost como estaba
      # sólo hay que añadir las siguiente directivas: Proxy y ProxyPass

      <Proxy balancer://mycluster>
          # Server 1
          BalancerMember http://IP-HTTP-SERVER-1:8081

          # Server 2
          BalancerMember http://IP-HTTP-SERVER-2:8082

          # Server 3
          BalancerMember http://IP-HTTP-SERVER-3:8083

          # Server 4
          BalancerMember http://IP-HTTP-SERVER-4:8084
      </Proxy>

      ProxyPass / balancer://mycluster/
      </VirtualHost>

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2011.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2012.png)

Y hay que reemplazar IP-HTTP-SERVER-1, IP-HTTP-SERVER-2, IP-HTTP-SERVER-3 y IP-HTTP-SERVER-4 que habrá que poner localhost para la máquina que estamos utilizando.

  ### 3. FUNCIONAMIENTO

Ahora, comprobamos si los siguientes parámetros que hemos puesto funcionan a la perfección:

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2013.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2014.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2015.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2016.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2017.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2018.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2019.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2020.png)

![](https://github.com/Jorgeev27/GIT/blob/main/img/Tarea%2020%20-%20Balanceo%20de%20Carga%20en%20Apache/Balanceo%20Cargas%2021.png)
