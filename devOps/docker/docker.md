ear
# Docker

## Table of Contents

- [Docker](#docker)
  - [Table of Contents](#table-of-contents)
  - [What is Docker ?](#what-is-docker-)
  - [Docker Hub](#docker-hub)
  - [Docker Commands](#docker-commands)
    - [Auth](#auth)
    - [Images](#images)
    - [Containers](#containers)
  - [Dockerfile](#dockerfile)
  - [Docker Compose](#docker-compose)
    - [YAML Configuration Files](#yaml-configuration-files)
    - [YAML Instructions](#yaml-instructions)
    - [Commands](#commands)
  - [Docker Volumes](#docker-volumes)
  - [Docker Network](#docker-network)

## What is Docker ?

Docker is an open platform for developing, shipping, and serving `containers` (`Virtual Environments`). It enables you to isolate your applications between each other and from your infrastructure. It was originally created by the French developer *Solomon Hykes* in 2013. Today, it is the most popular platform used by companies for running applications. Docker uses the **Docker engine** to run containers.

Docker containers relie on LXC (LinuX Containers) which is a feature of the Linux Kernel. People use Docker for its portability.

![img_1](/devOps/docker/resources/logo.jpg)

## Internal Mechanisms

Docker uses the **Docker Daemon**

![img_2](/devOps/docker/resources/docker-components.png)

## Docker Hub

Docker Hub is the official repository that stores all publicly available Docker **images**. It is accessible via the following URL: https://hub.docker.com/

## Docker Commands

### Auth

```bash
docker login --username=my_username
```

### Images

**Docker Image**: read-only file with a bunch of instructions. When these instructions are executed, it creates a Docker container.

An image can be seen as a snapshot from a program. It is a template used for building a container.

Build a Docker image (need to be in the Dockerfile directory)
```bash
docker build . -t my_image_tag
```

Show all downloaded/local images
```bash
docker images
```

Delete all images
```bash
docker rmi -f $(docker images -aq)
```

Tag an image (before pushing it to the Docker Hub)
```bash
docker tag 5bca1327c754 williammadie/cours-montreuil:num_version
```

Push an image (needs to be tagged before)
```bash
docker push williammadie/cours-montreuil:firsttry
```

Get an image
```bash
docker pull williammadie/cours-montreuil:firsttry
```

### Containers

A container is **an instance of an image**. It can be executed several times simultaneously on a machine.

Show active Docker containers
```bash
docker ps

CONTAINER ID   IMAGE           COMMAND             CREATED       STATUS                     PORTS     NAMES
917a6c16b7df   tomcat:latest   "catalina.sh run"   3 weeks ago   Exited (143) 3 weeks ago             TomcatContainer
```

Show all (active and inactive) Docker containers 
```bash
docker ps -a
```

Run a Docker container and execute a command
```bash
docker run --name=container_name -it image_name cmd

# Example:
docker run -it ubuntu bash # run a container Ubuntu and execute a shell

# -i => interactive
# -t => in terminal
```



Run a detached Docker container
```bash
docker run --name=container_name -d image_name
```

Rename a Docker container
```bash
docker rename old_container_name new_container_name
```

Stop all Docker container
```bash
docker stop $(docker ps -aq)
```

Delete a specific Docker container
```bash
docker rm container_name
```

Remove all Docker container
```bash
docker rm $(docker ps -aq)
```

See logs from a specific Docker container (-f for follow)
```bash
docker logs container_name -f
```

See current settings of a Docker container
```bash
docker inspect container_name
```

Get inside the container and specificly in a shell
```bash
docker exec -it container_magique /bin/bash
```

## Dockerfile

Docker can build images automatically by reading the instructions from a `Dockerfile`. This file contains all the commands a user could call on the command line to assemble an image.

Format of a Dockerfile
```docker
# Comment (MUST BE on their own line : no instructions allowed on the same line as a comment)
INSTRUCTION arguments
```

Please note that instructions are not case-sensitive but should be written in uppercase to distinguish them from arguments more easily.

### Structure of a Dockerfile

An example of Dockerfile (create an image for an Angular website running with NGINX)
```docker
#stage 1
FROM node:latest as node
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod#stage 2
FROM nginx:alpine
COPY --from=node /app/dist/demo-app /usr/share/nginx/html
```

What the hell is that ?? Let's detail it:

1. Specify the parent image from which we are building the image. A `FROM` instruction can be used several time and then accessed with the `--from` argument.
**A valid Dockerfile must begin with FROM**
```docker
FROM parent_image
```

2. Specify the working directory of the project. This is used to define the working directory of the container. Docker will execute the following commands from this file.
```docker
WORKDIR working/dir/path
```

3. Copy files from a **local source** to a **destination** in the Docker container. Here, it will copy all files located in the project working directory into the previously defined **working directory** of the Docker container.
```docker
COPY project/filepath container/filepath
``` 

4. Launch prerequisites commands for image building
```docker
RUN my image setup command
```

Do not confuse the `RUN` command with the `CMD` command!!
- `RUN`: command triggered while Docker is building the image
- `CMD`: command triggered while Docker launch the created image

It can be only one **CMD** command in a Dockerfile (generally in last). If there are multiple `CMD` commands, only the last one will be executed. (See below example for usage)

A second example
```docker
FROM python:3.9-slim-buster
WORKDIR /app
COPY ./requirements.txt /app
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
ENV FLASK_APP=my_flask.py
CMD ["flask", "run", "--host", "0.0.0.0"]
```

1. We base our customized image on the `python:3.9-slim-buster` image.
2. We specify the container workdir `/app`.
3. We copy the `requirements.txt` (which is not in the `app` folder) in the `app` folder.
4. We run a dependency installation command. It is required for our image to work.
5. We copy all the content of our current working directory (directory of the Dockerfile) in the working directory of the container (`/app`).
6. We expose the port `5000` of the container. It is required for the OS to communicate with the container.
7. We set the `FLASK_APP` environment variable required for the flask application to run.
8. We add the run command of the application.

## Docker Compose

Docker Compose is a module based on Docker. It was firstly developped aside from Docker and has been fully integrated to Docker later.

Historically, it was `docker-compose` then it became `docker compose`.

It is used to facilitate the configuration of `multi-containers` applications.

Docker commands look up for `all known containers/images` whereas Docker Compose looks up for `containers/images` inside the folder of the `docker-compose.yml` file

### YAML Configuration Files

In order to set up a Docker container more easily, we use **YAML configuration files** which allow us to configure our container with a light syntax and explicit settings. It also enables us to configure the container's environment variables for our applications.

```yaml
version: '3'

services:
    db:
        image: mysql:5.7
        columes:
            - db_data:/var/lib/mysql
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: passwd
            MYSQL_DATABASE: wordpress
            MYSQL_USER: wordpress
            MYSQL_PASSWORD: wordpress
```

### YAML Instructions

Indicate that this container needs other containers to be up and running to work
```yaml
services:
  my-service:
    ...
    depends_on:
      - db
```

Use a volume with a Docker Container
```yaml
services:
  my-service:
    volumes:
      - ./data/db:/var/lib/postgresql/data
      - host/path:container/path
```

### Commands

Create a detached Docker container
```bash
docker-compose up -d
```

Destroy a Docker container
```bash
docker-compose down
```

Launch a Docker container (quicker than up)
```bash
docker-compose start
```

Stop a Docker container (quicker than down)
```bash
docker-compose stop
```

## Docker Volume

`volume`: mechanism used for persisting data generated by Docker Containers.

A volume is a repository used in the host filesystem to store information related to a container.

![volume](/devOps/docker/resources/docker-volumes.jpg)

## Docker Network

It is possible to create networks of containers. These containers can communicate together.

![network](/devOps/docker/resources/docker-networks.jpg)