# Tarea 21: Balanceo de Carga en Nginx

  ## Jorge Escobar Viñuales

  ## Indice:
 - Configuración de un Dominio en Nginx
 - Funcionamiento

 ### 1. CONFIGURACIÓN DE UN DOMINIO EN NGINX

Hay que tener instalado y activado Nginx.

Hay que crear un archivo de VirtualHost dentro de sites-available con el siguiente comando:

    sudo nano /etc/nginx/sites-available/midominio.com.conf

Y editamos el archivo añadiendo la configuración para el proxy inverso:


    server {
        #Escucha en el puerto 8090, ipv4.
        listen 8090;

        #Aquí deberás introducir el nombre de tu dominio.
        server_name midominio.com;

        access_log            /var/log/nginx/midominio.com.access.log;

        location / {
            #La configuración del proxy.
            proxy_pass http://localhost:8083/app-web-demo/;
        }
    }


Reiniciamos Nginx:

    sudo systemctl reload nginx

Accedemos a midominio.com e indicamos la respuesta.

Ahora, vamos a añadir más configuración y ver el comportamiento de esta:

    http {
        upstream server_group_wildfly {
            least_conn;
            server http://localhost:8081/app-web-demo/;
            server http://localhost:8082/app-web-demo/;
            server http://localhost:8083/app-web-demo/;
            server http://localhost:8084/app-web-demo/ backup;
        }

        server {
            location / {
                proxy_pass http://server_group_wildfly;
            }
        }
    }


La directiva least_conn en el grupo de hosts llamado backend define que NGINX envíe las peticiones entre los servidores localhost 8081-8082-8083, dependiendo de que el host tenga el menor número de conexiones activas. NGINX utiliza el servidor localhost:8084 sólo como respaldo en caso de que los otros dos hosts no estén disponibles.

 ### 2. FUNCIONAMIENTO
