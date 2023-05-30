# Introduction to Docker

## Create a docker container
```
docker run -i -t ubuntu /bin/bash
```

docker run - to start up a docker container

-i - to keep STDIN (Standard Input) open to the container even if it hasn't been attached

-t - Assign a pseudo-tty to the container we are about to create

This therefore creates an interactive shell to the container
This helps interact with the container via a command line rather than a daemonized service

## View docker containers
```
#view running docker images
docker ps -aux
#list all docker containers
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
## Inspect container processes
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

