# Tarea 19: Desplegar una aplicación en Node.js en Docker

  ## Jorge Escobar Viñuales

  ## Indice:
 - Introducción
 - Creacoón del Node.js App
 - Creación del Archivo Dockerfile
 - Creación del Archivo .dockerignore
 - Creando la imagen
 - Correr la imagen

 ### 1. INTRODUCCIÓN

Lo primero que hay que hacer es instalar nodejs como npm. Para ello utilizamos los comandos:

    curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
    sudo apt-get install -y nodejs

Después de ello, podemos realizar la tarea.


  ### 2. CREACIÓN DEL NODE.JS APP

En el mismo directorio donde vamos a realizar la tarea, creamos un archivo package.json para describir nuestra app y dependencias:

    {
      "name": "docker_web_app",
      "version": "1.0.0",
      "description": "Node.js on Docker",
      "author": "First Last <first.last@example.com>",
      "main": "server.js",
      "scripts": {
        "start": "node server.js"
      },
      "dependencies": {
        "express": "^4.16.1"
      }
    }

Con nuestro archivo en marcha, hacemos el siguiente comando para que genere un archivo package-lock.json, que copia a nuestra imagen de Docker.

Después de esto, creamos un archivo server.js que define nuestra aplicación web:

    'use strict';
    const express = require('express');
    // Constants
    const PORT = 8080;
    const HOST = '0.0.0.0';
    // App
    const app = express();
    app.get('/', (req, res) => {
      res.send('Hello World');
    });
    app.listen(PORT, HOST);
    console.log(`Running on http://${HOST}:${PORT}`);

    Y con los siguientes pasos, veremos cómo se puede ejecutar la aplicación dentro del contenedor Docker usando la imagen oficial de ésta. Pero primero, habrá que crear la imagen de Docker para poder iniciar la aplicación.

  ### 3. CREACIÓN DEL ARCHIVO DOCKERFILE

Creamos un archivo llamado Dockerfile:

    FROM node:16

    # Create app directory
    WORKDIR /usr/src/app

    # Install app dependencies
    # A wildcard is used to ensure both package.json AND package-lock.json are copied
    # where available (npm@5+)
    COPY package*.json ./

    RUN npm install
    # If you are building your code for production
    # RUN npm ci --only=production

    # Bundle app source
    COPY . .

    EXPOSE 8080
    CMD [ "node", "server.js" ]

    ### 4. CREACIÓN DEL ARCHIVO .DOCKERIGNORE

Creamos un archivo .dockerignore  en el mismo directorio donde hemos creado los anteriores:

    node_modules
    npm-debug.log

Esto hace que los módulos locales y registros de depuración se copien en su imagen de Docker y posiblemente sobrescribir los módulos instalados dentro de la imagen de Docker.

    ### 5. CREANDO LA IMAGEN

Vamos al directorio que tenemos el Dockerfile y ejecutamos el siguiente comando para crear la imagen de Docker:

    docker build . -t <your username>/node-web-app

El -t del comando nos permite etiquetar nuestra imagen para que sea más fácil de encontrar más tarde usando el comando docker images:

Con ello, ya así tenemos la imagen de Docker:

    $ docker images
    # Example
    REPOSITORY                      TAG        ID                  CREATED
    node                            16         3b66eb585643    5 days ago
    <your username>/node-web-app    latest     d64d3505b0d2    1 minute ago

    ### 6. CORRER LA IMAGEN

Ejecutamos la imagen que se creó anteriormente:

    docker run -p 49160:8080 -d <your username>/node-web-app

Ejecutando el comando con -d que lo ejecuta por separado, dejando el contenedor ejecutándose en un segundo plano. El comando -p redirige el puerto público a un puerto privado dentro del contenedor.

Ejecutamos la salida de la app con los comandos:

    # Get container ID
    $ docker ps
    # Print app output
    $ docker logs <container id>
    # Example
    Running on http://localhost:8080
