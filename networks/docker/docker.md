# Docker

## Table of Contents

- [What is Docker ?](#what-is-docker)
- [Docker Hub](#docker-hub)
- [Docker Commands](#docker-commands)
    - [Auth](#auth)
    - [Images](#images)
    - [Containers](#containers)
- [Docker Compose](#docker-compose)
    - [YAML Configuration Files](#yaml-configuration-files)
    - [Commands](#commands)

## What is Docker ?

Docker is an open platform for developing, shipping, and serving containers. It enables you to isolate your applications between each other and from your infrastructure. It was originally created by the French developer *Solomon Hykes* in 2013. Today, it is the most popular platform used by companies for running applications. Docker uses the **Docker engine** to run containers.

![img_1](/networks/docker/resources/logo.jpg)

## Docker Hub

Docker Hub is the official repository that stores all publicly available Docker **images**. It is accessible via the following URL: https://hub.docker.com/

## Docker Commands

### Auth

```bash
docker login --username=my_username
```

### Images

Build a Docker image (need to be in the Dockerfile directory)
```bash
docker build . -t my_image_name
```

Show all downloaded/local images
```bash
docker images
```

Delete all images
```bash
docker rmi -f $(docker images -a -q)
```

Tag an image (before pushing it to the Docker Hub)
```bash
docker tag 5bca1327c754 williammadie/cours-montreuil:num_version
```

Push an image (needs to be tagged before)
```bash
docker push williammadie/cours-montreuil:firsttry
```

### Containers

Show active Docker containers
```bash
docker ps
```

Show all (active and inactive) Docker containers 
```bash
docker ps -a
```

Run a Docker container
```bash
docker run --name=container_name -it image_name cmd
```

Run a detached Docker container
```bash
docker run --name=container_name -d image_name
```

Rename a Docker container
```bash
docker rename old_container_name new_container_name
```

Delete a specific Docker container
```bash
docker rm container_name
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

## Docker Compose

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

