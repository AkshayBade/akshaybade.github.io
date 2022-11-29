---
---
# Learn Docker

1. [What is Docker](#what-is-docker)
2. [Why to use Docker](#why-to-use-docker)
3. [How Containers Work](#how-containers-work)
4. [Local installation](#local-installation)
5. [Sample Example](#sample-example)
6. [Basic Operations](#basic-operations)
7. [Demo Project](learn_docker_demo.md/#setup)
8. [FAQ](#faq)

## What is Docker
Docker helps you create a package of your application along with its all possible dependencies required to run that application.

## Why to use Docker
This solves problems like,
1. "works on my machine" problems
2. No need to spend redundant efforts of setting up development infra like installing softwares needed to run your application on local along with compatible versions and OS compatibility.
3. Package with all needed configurations
4. Multiple applications can now run in their own containerized environment without conflicting with other applications and their softwares dependencies
5. Makes Deployments faster by removing redundancy of following same installations steps on every environment.
6. 

## How Containers Work
Unix namespaces:
Unix chroot: complete file system comes under docker image. Container adds additional isolation using chroot to this file system.


## Local installation
Install Docker Desktop.
https://docs.docker.com/desktop/install/ubuntu/

## Terminologies
#### Docker daemon
Continous running instance which takes instructions to perform actions on docker image.
#### Docker cli
A client which exposes commands to be run to interact with docker engine.
#### Docker Repository
Location at which docker images can be stored and managed for distribution (public / private)
- Docker image repository
https://docs.docker.com/desktop/install/ubuntu/#install-docker-desktop


## Sample Example
Run hello world image on docker.
1. Start docker daemon
```console
sudo dockerd
```
2. Run hello world image
```console
$ sudo docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
.
.
.
$
```

## Basic operations
#### Check locally available images
```console
$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
hello-world   latest    feb5d9fea6a5   14 months ago   13.3kB
$
```
#### pull image
```console
$ docker pull redis
Using default tag: latest
latest: Pulling from library/redis
a603fa5e3b41: Pull complete
77631c3ef092: Pull complete
ed3847cf62b8: Pull complete
261a8b530567: Pull complete
7d9005a8af6d: Pull complete
828da1afb5be: Pull complete
Digest: sha256:1e3207c292225b6dd21cb74d59255748a50e8f739dd983040df38fa913927cf1
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest

$ docker image ls
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
redis         latest    3358aea34e8c   2 weeks ago     117MB
hello-world   latest    feb5d9fea6a5   14 months ago   13.3kB
$
```
#### Check Running Containers
```console
$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS      NAMES
9e889699203c   redis     "docker-entrypoint.s…"   47 seconds ago   Up 46 seconds   6379/tcp   determined_hellman
$
```
Docker containers can make run in detached mode with below cmd
```console
$ sudo docker run -d redis
```
#### Stop container
```console
$ sudo docker stop <CONTAINER_ID>
$ sudo docker stop 9e889699203c
$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS      NAMES
$ sudo docker start 9e889699203c
.
.
.
$
```
#### See list of running + non-running containers
```console
$ sudo docker ps -a
CONTAINER ID   IMAGE         COMMAND                  CREATED          STATUS                      PORTS      NAMES
9e889699203c   redis         "docker-entrypoint.s…"   6 minutes ago    Up 6 minutes                6379/tcp   determined_hellman
413b679579b6   hello-world   "/hello"                 12 minutes ago   Exited (0) 12 minutes ago              stupefied_ramanujan
f0629920ab82   hello-world   "/hello"                 23 hours ago     Exited (0) 23 hours ago                brave_nightingale
$
```

#### Access Running container services
#### Port binding
I need to bind the running container port with server/host port to make it accessible outside container.
```console
$ sudo docker run -d -p6000:6379 redis
$
$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                       NAMES
dd28f2513189   redis     "docker-entrypoint.s…"   13 seconds ago   Up 13 seconds   0.0.0.0:6000->6379/tcp, :::6000->6379/tcp   priceless_gauss
$
```

### Debug commands
#### Check logs for container
```console
$ docker logs <CONTAINER_ID>
$ docker logs dd28f2513189
```

#### Get inside container file system
```console
# docker exec -it dd28f2513189 /bin/bash
root@dd28f2513189:/data# cd ..
root@dd28f2513189:/# ls
bin  boot  data  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@dd28f2513189:/#
```
*** Now since we are inside container, it will not have any of shell commands ready to use since those are not installed for that container.

## FAQ
1. What is Docker GPG key & why do we need it?
-> Check docker forum for same: https://forums.docker.com/t/difference-between-docker-desktop-and-docker-engine/124612
2. How is Docker-desktop different from Docker engine, cli packages?
