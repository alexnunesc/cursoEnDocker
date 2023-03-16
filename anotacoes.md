# Docker, qué es?

https://www.youtube.com/watch?v=4Dko5W96WHg&t=1296s

Es un contenedor.

__Una caja que podemos mesclar y guadar nuestras aplicaciones.__

### ejemplo.

caja.
HTML
Node.js
.env

Esos contenedores son portables.


# Donde se almacenar?

***Docker Hub. Similar a GitHub.***


# Docker descktop.
  -01 Una maquina vitual que corre linux.
  -02 CLI linea de comando.

# Intalacion


# Comandos Dockers.

Mirar las imagenes >> docker images.

Descargar los imagenes >> docker pull nameImageVersion.
  Ex. node:16

Eliminar imagenes >> docker image rm nameImage:version.
  Ex. node:18

Crear contenedor >> docker create nameImage.
  Ex. mongo
  >> salva id 1ac678d873bbb4c96684ea88954b4737ca48705d162751e2715df5c172fd8fbd

Iniciar el contenedor
  >> docker start id.

Verificar se esta corriendo.
  >> docker ps. o docker ps -a.

Cerrar el contenedor.
  >> docker stop id.

Eliminar el contenedor.
  >> docker rm nameContenedor.

Crear contenedor con um nombre especifico >> docker create --name nameDeseado nameImage.
  Ex. docker create --name mondoDb01 mongo


Port mapping.
  host
  port 3000 node.
  port 3001 node.
  port 27017 mongo.
estos puertas poden ser variables. ex 27018.

Creando contenedores con puertas.

 docker create -p27017:27017 --name monguito mongo.

Verificando los logs. >> 
>> docker logs name. o docker logs --follow name.

Creando y corriendo.
  >> docker run -d mongo. 
  >> docker run --name monguito -p27017:27017 -d mongo.

Configurando contenedor mongo.
https://hub.docker.com/_/mongo
>>  docker create -p27017:27017 --name monguito -e  MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo

53min


Verificar las redes.
  >> docker network ls.

Crear rede.
  >> docker network create nameRede.

Eliminar rede.
  >> docker network rm naemRede.


Creando.
  crenado archivo Dockerfille
  **
  FROM node:16

  RUN mkdir -p /home/app

  COPY . /home/app

  EXPOSE 3000

  CMD ["node", "/home/app/index.js"]
  **

  crebado app.
  >> docker build -t miapp:1 .
  crenado bd com rede.
  >> docker create -p27017:27017 --name monguito --network mired  -e  MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo

  creando el contenedor.
  >> docker create --name chanchito --network mired miapp:1

Start.
  >> start monguito 
  >> start chanchito

Crear achirvo docker-compose.yml.
  >>
  version: "3.9"
  services:
    chanchito:
      build: .
      ports:
        - "3000:3000"
      links:
        - monguito
    monguito:
      image: mongo
      ports:
        - "27017:27017"
      environment:
        - MONGO_INITDB_ROOT_USERNAME=nico
        - MONGO_INITDB_ROOT_PASSWORD=password
      volumes:
        - mongo-data:/data/db
        # mysql -> /var/lib/mysql
        # postgres -> /var/lib/postgresql/data

  volumes:
    mongo-data:



Comando.
  >> docker compose up.

Elimindado.
  >> docker compse down.



Volumes.

  anonimo: indicar rota.
  host: incidar a rota.
  nombrado:
  
  Ex.
  >> volumes:
      - mongo-data:/data/db
