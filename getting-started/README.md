# Introduction to Docker
## What is a docker?
Docker is an open platform for developing, shipping, and running applications
## What is containerization?
Containerization in application development is a way of packaging our application enhancing portability and maintaining consitency in application.
## The docker components
- The docker client and server (Docker engine)
- Docker images
- Registries
- Docker containers

### The docker engine
The docker engine is a client-server application. The client talks to the docker server or daemon.
Docker ships with a docker client and a RESTful API to interact with the daemon: dockerd

### Docker images
A Docker image is an executable package of software that includes everything needed to run an application. 

Docker images act as a set of instructions to build a Docker container, like a template
### Registries
Registries in docker are private or public docker images uploaded to the docker hub by the image owners.

Docker hub is a website by the docker company where users can access private or public images (Registries) 

### Docker container
A Docker container is a standardized unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another 

## Creating a docker container
You can create a docker container from a docker image stored on your local machine or on a private/public docker registry.
```
docker run -i -t ubuntu /bin/bash
```

docker run - it is used to start up a docker container

-i - this flag is used to keep STDIN (Standard Input) open to the container even if it hasn't been attached

-t - this flag assigns a pseudo-tty to the container we are about to create

This therefore creates an interactive shell to the container
This helps you interact with the container via a command line rather than a daemonized service

## View docker containers
```
#view running docker images
#List of current containers
docker ps -a
docker ps -aux
#list last run container whether it is in running or stopped state
docker ps -l 
```

## Naming a docker container
Docker uses a randomly generated name for containers when created.
To specify a name we use the --name option.
```
docker run --name=test-container -i -t ubuntu /bin/bash
```

## Starting and stopping a container
A docker container can be started or stopped using the name or id of the conatiner
```
docker start <container-name>
docker stop <container-name>
```
## Attaching to containers
An interactive session is created on running a container. We can attach back to that interactive session using 
```
docker attach <container-name or container-id>
```
## Fetch logs of a container
```
docker log <container-name>

# monitor the logs like tail -f
docker log -f <container-name>

# prefix logs with timestamps
docker log -tf <container-name>
```
## Docker statistics - Inspect container processes
```
docker top <container-name>

# using docker inspect
docker inspect <container-name>
```

## Running a process inside an already running process
We can run additional processes inside a container using docker exec

Run a background process inside a container
```
 sudo docker exec -d <container-name> touch /etc/new_config_file
```
flag -d to specify it runs on the background

Run an interactive command inside a container (foreground process)
```
$ sudo docker exec -t -i daemon_dave /bin/bash
```

## Automatic container restarts
We can set a docker container to automatically restart on failure
```
docker run -i -t --name=my-ubuntu --restart=on-failure ubuntu \bin\bash
# here are some restart options
# --restart=always
# --restart=on-failure (restarts if the container exists with a non zero exit code)
# --restart=on-failure:5 (optional restart-count)
```

## Docker inspect
We can get a whole lot more information using docker inspect
```
docker inspect <docker-id/name>
## We can query the results using -f or --format
```

## Removing docker containers
```
docker rm <docker-id/name>
```
You can also delete all containers by querying container ids
```
docker rm -f `sudo docker ps -a -q`
# -f - force remove even running containers
# -a - list docker containers
# -q - list docker ids
```

