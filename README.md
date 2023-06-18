# Docker

## Table of Contents

-   [Introduction](#introduction)
-   [Linux and Networking](#linux-and-networking)
-   [Commands](#commands)
    -   [Miscellaneous Commands](#miscellaneous-commands)
    -   [Images](#images)
    -   [Containers](#containers)
    -   [Bind Mount](#bind-mount)
-   [Resources](#resources)

## Introduction

-   Crash course
    -   [Exploring Docker [1] - Getting Started](https://www.youtube.com/watch?v=Kyx2PsuwomE)
    -   [Exploring Docker [2] - Docker Compose With Node & MongoDB](https://www.youtube.com/watch?v=hP77Rua1E0c)
-   [Docker in 100 secs](https://www.youtube.com/watch?v=Gjnup-PuquQ)
-   Aim: To run software services/progs/applications inside containers.
-   Eg: Apache, MySQL, MongoDB, NginX (web server common to Apache), Wordpress, etc...
-   Advantages: Convenient, fast, simple, easy to re-create the same environment.
-   [Docker Hub](https://hub.docker.com) == GitHub of Docker

> NOTE:
>
> -   [Docker Desktop for Windows Home is here!](https://www.docker.com/blog/docker-desktop-for-windows-home-is-here)
> -   For Win 10 Home (2004 and above), Pro and Enterprise, install Docker Desktop.
> -   For Win 10 Home 1909 and lower, install Docker Toolkit.
> -   Docker might not work on VSCode integrated terminal. In that case, open VSCode as an administrator, use ext cmd or use powershell.
> -   Some commands might not work in cmd. Use Powershell in that case.
> -   [`$(pwd)` in MacOS is `$(%cd%)` in Cmd and `${PWD}` in Powershell](https://stackoverflow.com/questions/41485217/mount-current-directory-as-a-volume-in-docker-on-windows-10)
> -   `localhost:port` might not work. Use `198.168.99.100:port` instead.
> -   Container privileges
>     -   [Network privileges might be required sometimes](https://unix.stackexchange.com/questions/459206/list-ip-tables-in-docker-container)
>     -   [All privileges](https://stackoverflow.com/questions/36425230/privileged-containers-and-capabilities)

## Linux and Networking

Please refer to [linux-networking.md](linux-networking.md).

## Commands

### Miscellaneous Commands

-   `docker version`
-   Server: Docker Engine (built on Go lang)
-   `docker info`

### Images

-   To view images on local machine: `docker images`
-   To remove images: `docker image rm ed2` (the entire image ID is not required)
-   To pull image from DockerHub: `docker pull nginx`
-   To build image
    -   `docker image build -t harshkapadia/nginx-website .`
        -   `harshkapadia/nginx-website` = Docker_ID/img_name
        -   `.` = refering to Dockerfile in currect dir (make sure your cmd is pointing to the correct folder)
-   To push image to DockerHub: `docker push harshkapadia/nginx-website`

### Containers

-   To show running containers
    -   `docker container ls`
    -   `docker container ps`
    -   `docker ps`
-   To show all containers on the system
    -   `docker container ls -a`
    -   `docker ps -a`
-   To run container in the foreground
    -   `docker container run -it -p 80:80 --name my_custom_name_for_nginx nginx`
        -   `container` = management command
        -   `run` = sub-command
        -   `it` = interactive terminal, ie, run in the foreground
        -   `-p` or `--publish` = publish
        -   `80:80` = mapping ports (port*to_be_used_on_local_machine*(use*any_port):port_exposed_from_container*- (use_default_port_of_service_in_container))
        -   `nginx` = image name
    -   Once the img is downloaded:
        -   `localhost:80` or `localhost` (default is 80) or `127.0.0.1` (localhost)
        -   Win 10 Home users (might not be needed with Docker Desktop): `192.168.99.100` (Since Toolbox is running a Linux VM in VirtualBox, localhost won't work. Use `192.168.99.100` (default) instead.)
    -   To stop container: <kbd>ctrl</kbd> + <kbd>c</kbd>
-   To run container in the background:
    -   `docker container run -d -p 8080:80 --name my_custom_name_for_nginx nginx`
        -   `-d` or `--detach` = detached
    -   To stop container: `docker stop my_custom_name_for_nginx` or `docker container stop my_custom_name_for_nginx`
    -   To view:
        `192.168.99.100:8080` (Win 10 Home users - might not be needed with Docker Desktop - `localhost` might work)
-   To remove container: `docker container rm c699` (the entire container ID is not required) (deleting container does not remove the image from the system)
-   To remove running container:
    -   First stop the container and use the remove command
    -   OR use force: `docker container rm c699 -f`
-   To remove all containers on the system: `docker rm $(docker ps -aq) -f` (`-f` added to remove any running container(s) as well) (this ran in powershell, but not in cmd)
-   Env variables: `docker container run -d -p 3306:3306 --name my_sql_user --env MYSQL_ROOT_PASSWORD=123456 mysql` (you can find the env vars on Docker Hub)
-   To start a new container from an existing image: `docker container run -d -p 80:80 --name custom_name_nginx nginx`
-   To start an existing container: `docker start <container_id>`
-   To enter a container: `docker container exec -it mynginx bash` (start the container using the abv cmd before doing this)
    -   After entering:
        -   To view file system: `ls`
        -   To get to index.html (displayed on screen at port) (for nginx): `cd usr/share/nginx/html`
        -   To come out of container: `exit`
        -   To edit file, refer to the bind mount section below.

### Bind Mount

> NOTE: Ports 80 or 8081 might not work with below example. Use 8080, 8082, 8083...

-   To create container:
    -   With Docker Toolbox:
        -   Refer to [`bind_mount.md`](bind_mount.md) for further details on 'x_drive'.
        -   Make sure docker-machine is running (`docker-machine start`)
        -   `docker container run -d -p 8080:80 -v /x_drive/coding/docker/docker_basics/mounting_example:/usr/share/nginx/html --name - nginx-website nginx`
        -   Refer to files in the [`mounting_example`](mounting_example) folder.
    -   With Docker Desktop:
        `docker container run -it -v "%cd%":/mnt --name kali kalilinux/kali-rolling`

## Resources

-   [Understanding Docker layers](https://devops.stackexchange.com/questions/1750/understanding-docker-layers)
-   [Networking in a Linux Container in Docker](linux-networking.md)
-   [Linux file system](https://gist.github.com/HarshKapadia2/18150e1e57eab1f0e500f18feea890aa)
-   [Linux Terminal commands](https://harshkapadia2.github.io/cli)
-   [Windows Subsystem for Linux](https://gist.github.com/HarshKapadia2/714bba15f0f09d32c07cdde3c244be9f) (WSL)
-   [Windows Terminal](https://gist.github.com/HarshKapadia2/18daf23ab4a7d1cb9215ca9dc8b7099f) (WT)
