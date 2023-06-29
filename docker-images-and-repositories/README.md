# Docker Images and docker repository
## View docker images on your local machine
```
docker images
```
## Pull docker image (i.e., ubuntu image with the tag)

A tag of an image can be the version of the image or a representation to help get a specific image
```
docker pull ubuntu:18.04
```
You can narrow down your image search by specifying a specific image (i.e., local ubuntu images)
```
docker images ubuntu
```
## Search for docker image
You can search for publicly available images using docker search from docker hub
```
docker search <image-name>
```

## Building docker images
We generally build images from base images (i.e., Ubuntu, alphine, Apache)
## Signing into docker hub
```
docker login 
#logging out of docker use
docker logout
```
When we sign in the configuration is store in our home directory under /home/.docker/config

It is recommended to use docker a dockerfile to build docker image.

The docker build command builds an images from a file. In the example below we build a file in the same directory (.Dockerfile)

-t - this tag is used to define the name of the image. With name of the user followed by the image name, followed by a tag.

If you miss to add a tag, docker automatically tags it as latest
```
docker build -t="jamtur01/static_web:v1" .
# You can also specify the file from a URL
```
Docker uses cache to build images faster, therefore when you need docker to freshly start building your image add the --no-cache option
```
docker build --no-cache -t="jamtur01/static_web:v1" .
```
## Seeing how the docker image was build
```
docker history <docker-id/name>
```
The docker history command highlights how the image layers were build by docker allowing you to verify if the image was build well as describe by the Dockerfile

## Docker port
When an image is run you can use the docker port command to see the port opened for a container
```
docker port <container-id/container-name>
```
## Bind docker to some random port on docker host
```
docker run -d -p 127.0.0.1::80 --name=<container-name> <user/image-name> command
```
## We can view the exposed container using curl
```
curl localhost:<port>
```
## Examples of commands specified in a dockerfile
- CMD - Specifies the command run when the container is run. A good example is a java application (i.e, java -jar <application-jar.jar>).
Command is run at container runtime


**YOU CAN ONLY SPECIFY ONE CMD. If you specify more than one, the last CMD is run**
- RUN - Specify the command when the image is being build. This is when running the docker build command.
Command is run at conatiner build

**NOTE: It is recommend to write commands in array format.
Here are examples of array formats below**
```
CMD ["java", "-jar", "application-jar.jar"]
RUN ["apt-get", "install", "-y", "nginx" ]
```
- ENTRYPOINT - ENTRYPOINT it similar to **CMD** but has a slight difference. **CMD** commands can be overriden when docker run is run with commands at the end. 
**ENTRYPOINT** commands on the other hand cannot be overwritten.

In the example above `java -jar` command it is prefered to run it with entrypoint. Meaning that the command `java -jar` cannot be overwritten on docker run.
```
ENTRYPOINT ["java", "-jar"]
CMD ["application-jar.jar"]
```
The example above describes a neat example which allows us to override the `application-jar.jar` part to add extra commands at runtime.
```
docker run -d -p 8080:81 --name=my-java-app <user/image-name> -DEBUG=TRACE application-jar.jar
```
In the example above we have overriden the dockerfile by running the jar with a debug option

If you really need to overwrite the entrypoint you can run docker with the --entrypoint flag

- WORKDIR 

`WORKDIR` is used to set the working directory for a container or a specific instruction.
```
#Setting a working directory for an instruction & container

WORKDIR /opt/webapp/db
RUN bundle install
WORKDIR /opt/webapp
ENTRYPOINT [ "rackup" ]
```
We can also override the working directory for a container
```
sudo docker run -ti -w /var/log ubuntu pwd
/var/log
```

- ENV 

ENV is used to set environment variables during image build
```
ENV RVM_PATH /home/rvm/
```

- VOLUME

Used to add a volume to a container created using that specific image. Volumes are used for persistence and shared data storage.
```
VOLUME ["/opt/project"]
```

## Deleting an image
Deleting a docker image locally
```
sudo docker rmi <image-name>
```
Deleting all docker images
```
 sudo docker rmi `docker images -a -q`
```