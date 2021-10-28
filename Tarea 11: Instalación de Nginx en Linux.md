# Tarea 11: Instalación Nginx en Linux

  ## Jorge Escobar Viñuales

  ## Indice:
 - Instalación de Nginx
 - Aplicar los ajustes de Firewall
 - Comprobación del servidor web
 - Administrar el proceso de Nginx
 - Configurar los bloques del servidor (RECOMENDADO)
 - Familiarización con los archivos y directivos importantes de Nginx

Nginx es uno de los servidores web más populares del mundo y aloja algunos de los sitios más grandes y con mayor tráfico de internet. Es una opción ligera que se puede utilizar como servidor web o proxy inverso.

Instalaremos el servidor Nginx en Ubuntu, adaptando el firewall, administrando el proceso de Nginx y configurando los bloques del servidor para alojar más de un dominio desde un mismo servidor.


 ### 1. REQUISITOS PREVIOS

Como Nginx debe de estar disponible en los repositorios predeterminados de Ubuntu, es posible instalarlo desde los repositorios.

Utilizaremos el siguiente comando para tener el listado de los paquetes más recientes:

    sudo apt update

Ahora con esto listo, podemos instalar Nginx, con el siguiente comando:

    sudo apt install nginx

Tras haber aceptado todo el procedimiento, se instalará Nginx y cualquier dependencia necesaria en nuestra máquina virtual.

  ### 2. APLICAR LOS AJUSTES DE FIREWALL

Antes de probar Nginx, se debe ajustar y aplicar el software de firewall para permitir el acceso al servicio. Nginx registra de forma automática un servicio con ufw tras la instalación, por lo que lo hace más sencillo permitir el acceso.

Enumeramos las configuraciones de la aplicación con las que ufw sabe trabajar con el siguiente comando:

    sudo ufw app list

Y nos debería obtener un listado de los perfiles de la aplicación con el comando:

    Output
    Available applications:
      Nginx Full
      Nginx HTTP
      Nginx HTTPS
      OpenSSH

Y hay 3 perfiles para Nginx:

Nginx Full: Este perfil abre el puerto 80 (tráfico web normal, no cifrado), y el puerto 443 (puerto TLS/SSL cifrado.

Nginx HTTP: Este perfil abre solo el puerto 80 (tráfico web normal, no cifrado).

Nginx HTTPS: Este perfil abre solo el puerto 443 (tráfico TLS/SSL cifrado).

Se recomienda habilitar el perfil del puerto más restrictivo. En este momento, solo tendremos que permitir el tráfico en el puerto 80.

Se puede habilitar con el comando:

    sudo ufw allow 'Nginx HTTP'

Se puede verificar el cambio con el comando:

    sudo ufw status

Y el resultado indicará el tráfico de HTTP que se permite:

    Status: active

        To                                 Action              From
        --                                 ------              ----
            OpenSSH                        ALLOW               Anywhere                  
            Nginx HTTP                     ALLOW               Anywhere                  
            OpenSSH (v6)                   ALLOW               Anywhere (v6)             
            Nginx HTTP (v6)                ALLOW               Anywhere (v6)

### 3. COMPROBACIÓN DEL SERVIDOR WEB

Al final del proceso de instalación, Ubuntu iniciará Nginx. El servidor debería estar activo.

Realizamos una verificación para asegurarnos que el servicio se encuentra en ejecución con el comando:

    systemctl status nginx

Con la siguiente salida:

    ● nginx.service - A high performance web server and a reverse proxy server
        Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
        Active: active (running) since Fri 2020-04-20 16:08:19 UTC; 3 days ago
        Docs: man:nginx(8)
        Main PID: 2369 (nginx)
        Tasks: 2 (limit: 1153)
        Memory: 3.5M
        CGroup: /system.slice/nginx.service
                ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
                └─2380 nginx: worker process

Como nos confirma esto, el servicio se inició correctamente. Sin embargo, la mejor forma de comprobarlo es solicitando una página de Nginx.

En el caso de no salir activo, debe existir un problema de puertos, concretamente el puerto 80 debe de estar ocupado por otro servicio.

Hay que consultar el fichero logs, para verificar si el puerto está ocupado.

Puede acceder a la página de aterrizaje predeterminada de Nginx para confirmar que el software funcione correctamente dirigiéndose a la dirección IP del servidor. Si no conoce la dirección IP del servidor, se puede buscar con la herramienta icanhazip.com, que le proporcionará su dirección IP pública tal y como la recibió de otra ubicación de internet.

Para ello, ejecutamos el siguiente comando:

    curl -4 icanhazip.com

Cuando se tengo la dirección IP del servidor, introdúcela en la barra de direcciones del navegador:

    http://your_server_ip:puerto

Y debería de mostrarse que se ejecute correctamente Nginx.

Si está en la página, el servidor se está ejecutando correctamente y está listo para ser administrado.

### 4. ADMINISTRAR EL PROCESO DE NGINX

Ahora que el servidor está listo, revisamos algunos de los comandos básicos de la administración.

Para detener el servidor web, escribimos el comando:

    sudo systemctl stop nginx

Para iniciar el servidor web cuando no esté activo, escribimos el comando:

    sudo systemctl start nginx

Para detener y luego iniciar de nuevo servicio, escribimos el comando:

    sudo systemctl restart nginx

Si solo está realizando los cambios en la configuración, Nginx a menudo puede volver a cargarse sin perder las conexiones. Escribimos el comando:

    sudo systemctl reload nginx

De forma predeterminada, Nginx está configurado para iniciarse automáticamente cuando lo haga el servidor. Si no es lo que quiere, deshabilitamos este comportamiento con el siguiente comando:

    sudo systemctl disable nginx

Para volver a habilitar el servicio de modo que se cargue en el inicio, escribimos el comando:

    sudo systemctl enable nginx

Ya hemos aprendido los comandos de administración básicos y debería estar listo para configurar el sitio para alojar más de un dominio.

### 5. CONFIGURAR LOS BLOQUES DEL SERVIDOR (RECOMENDADO)

Al emplear el servidor web Nginx, se pueden utilizar bloques del servidor (similares a hosts virtuales de Apache) para encapsular los detalles de la configuración y alojar más de un dominio desde un único servidor. Configuraremos un dominio llamado your_domain (siendo your_domain el nombre de tu dominio o el que queramos).

Nginx en Ubuntu, tiene habilitado un bloque de servidor por defecto, que está configurado para suministrar documentos desde el directorio /var/www/html. Si bien funciona esto bien, puede ser difícil de manejar si aloja varios. En vez de modificar /var/www/html, vamos a crear una estructura de directorios dentro de /var/www para nuestro sitio your_domain y dejaremos /var/www/html como directorio predeterminado que se suministrará si una solicitud de cliente no coincide con otros sitios.

Entonces, vamos a crear un directorio para your_domain, usando -p para crear cualquier directorio principal necesario:

    sudo mkdir -p /var/www/your_domain/html

A continuación, asignamos la propiedad del directorio con la variable de entorno $USER con el comando:

    sudo chown -R $USER:$USER /var/www/your_domain/html

Los permisos del root deberían ser correctos si no se modifica el valor umask, que establece los permisos de archivos predeterminados. Para asegurarse de que los permisos sean correctos y permitir al propietario leer, escribir y ejecutar los archivos, y a la vez conceder sólo los permisos de lectura y ejecución a los grupos y terceros, pueden ingresar con el siguiente comando:

    sudo chmod -R 755 /var/www/your_domain

A continuación, crea una página de ejemplo index.html utilizando nano:

    sudo nano /var/www/your_domain/html/index.html

Dentro del html, agregamos el siguiente código html:

    <html>
        <head>
            <title>Welcome to your_domain!</title>
        </head>
        <body>
            <h1>Success!  The your_domain server block is working!
            </h1>
        </body>
    </html>

Para que Nginx presente el contenido, es necesario crear un bloque de servidor con las directivas correctas. En vez de modificar el archivo de configuración predeterminado directamente, se crea un nuevo en /etc/nginx/sites-available/your_domain:

    sudo nano /etc/nginx/sites-available/your_domain

Y pegarlo en el siguiente bloque de configuración, similar al predeterminado, pero actualizado para nuestro nuevo directorio y nombre de dominio:

    server {
            listen 80;
            listen [::]:80;

            root /var/www/your_domain/html;
            index index.html index.htm index.nginx-debian.html;

            server_name your_domain www.your_domain;

            location / {
                  try_files $uri $uri/ =404;
            }
          }

Hay que realizar este procedimiento sobre un puerto que tengamos disponible, en mi caso, el puerto 8086.

A continuación, habilitaremos el archivo creando un enlace entre éste y el dominio sites-enabled, en el cual Nginx obtiene las lecturas durante el inicio:

    sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/

Ahora contamos con los dos bloques de servidor habilitados y configurados para responder las solicitudes conforme a las directivas listen y server_name:

your_domain: Responde a las solicitudes de your_domain y www.your_domain.

default: Responde a cualquier solicitud en el puerto 80 que no coincida con los otros dos bloques.

Para evitar un problema de memoria de depósito de hash que pueda evitar surgir al agregar nombres de servidor, es necesario aplicar los ajustes a un valor en el archivo /etc/nginx/nginx.conf. Y abrimos el archivo con el comando:

    sudo nano /etc/nginx/nginx.conf

E intentamos encontrar la directiva server_names_hash_bucket_size y borre el símbolo # para eliminar el comentario de la línea. Para ello, con el comando:

    /etc/nginx/nginx.conf

Y buscamos server_names_hash_bucket_size:

    http {
        ...
          server_names_hash_bucket_size 64;
        ...
      }
    …

Guardamos el archivo y lo cerramos.

A continuación, comprobamos que no haya errores de sintaxis en ninguno de los archivos de Nginx. Con el comando:

    sudo nginx -t

Y si no hay problemas, reiniciamos Nginx para habilitar los cambios. Con el comando:

    sudo systemctl restart nginx

Con esto realizado, debería proporcionar el nombre de dominio. Podemos probarlo visitando ahttp://your_domain

### 6. FAMILIARIZACIÓN CON LOS ARCHIVOS Y DIRECTIVOS IMPORTANTES DE NGINX

/var/www/html: Contenido web real, que por defecto solo consta de la página predeterminada de Nginx.

/etc/nginx: Directorio de la configuración de Nginx. Se encuentran todos los archivos de configuración de Nginx.

/etc/nginx/nginx.conf: Archivo de configuración principal de Nginx. Se puede modificar para realizar cambios en la configuración general de Nginx.

/etc/nginx/sites-available/: Directorio en el que se guardan los bloques de servidor por sitio. Nginx no utilizará los archivos de configuración de este directorio a menos que estén vinculados al directorio sites-enabled. Normalmente, toda la configuración del bloque de servidor se realiza en este directorio y luego se habilita estableciendo un vínculo con el otro directorio.

/etc/nginx/snippets: Contiene fragmentos de configuración que pueden incluirse en otras partes de la configuración de Nginx. Los segmentos de configuración potencialmente repetibles reúnen las condiciones para la conversión a fragmentos.

/var/log/nginx/access.log: Cada solicitud al servidor web se registra en este archivo de registro, a menos que Nginx esté configurado para hacer algo diferente.

/var/log/nginx/error.log: Cualquier error de Nginx se asentará en este registro.

Una vez instalado este servidor web, hay muchas opciones respecto del tipo de contenido que ofrecerá y de las tecnologías que desee usar para crear una experiencia más completa.
