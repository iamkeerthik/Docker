Basic Docker Commands:

To see all images present in your local repo:
# docker images

To find out images in docker hub
# docker search image_name

To download image from dockerhub to local machine
# docker pull image_name

To give a name to container
# docker run -it --name new_name image_name /bin/bash

To check service start or not (status)
# docker service status

To start: #docker service start
To stop: # docker service stop

To start container
#docker start container_name

To go inside container
# docker attach container_name

To pause container
# docker pause <container_name>
# docker unpause <container_name>

To see all comtainers
# docker ps -a
or
# docker container ls -a

To see running containers
# docker ps
or
# docker container ls

To stop container
# docker stop container_name

To delete a container
# docker rm container_name

To delete a docker image
# docker rmi image_name
or
# docker image remove <image name>

Create container from our own Image:

Login into AWS account and start your EC2 instance, access it from putty.
Now we have to create container from our own image. Therefore, create one container first:

#docker run -it –name container_name image_name /bin/bash
#cd tmp/

Now create one file inside this tmp directory
# touch myfile

Now if you want to see the difference between the basic image and the changes on it
# docker diff container_name image_name

Now create image of this container
# docker commit newcontainer_name image_name
# docker images

Now create container from this image
# docker run -it --name newcontanier_name image_name /bin/bash
# ls# cd tmp
# ls (you will get all of your files)

     Dockerfile:
Dockerfile is basically a text file. It contains some set of instructions. Automation of docker image
creation.
Dockerfile components:

FROM: for base image, this command must be on the top of the dockerfile.
RUN: to execute commands, it will create a layer in image
MAINTAINER: author/ owner/ description
COPY: copy files from local system (docker vm) we need to provide source, destination (we can’t
download file from internet and any remote repo.)
ADD: similar to copy but it provides a feature to download files from internet, also extract file at
docker image side.
EXPOSE: to expose ports such as port 8080 for tomcat , port 80 for nginx etc.
CMD: execute commands but during container creation.
ENTRYPOINT: similar to CMD but has higher priority over CMD, first commands will be
executed by ENTRYPOIN only.
ENV: environment variables


Create a file named Dockerfile
Add instructions in Dockerfile
Build dockerfile to create image
Run image to create container

# vi Dockerfile
FROM ubuntu
RUN echo “kiriktech” > /tmp/testfile

To create image out of Dockerfile
# docker build -t myiamge

# docker images

Now create container from the above image
#docker run -it --name mycont myimage /bin/bash
#cat /tmp/testfile

ex2: #vi dockerfile
        FROM ubuntu
        WORKDIR /tmp
        RUN echo “thank you” > /tmp/testfile
        ENV myname kirik
        COPY testfile1 /tmp
        ADD test.tar.gz /tmp



Docker Volume:
Volume is simply a directory inside our container.
Finally, we have to declare this directory as a volume and then share volume.
Even if we stop the container still, we can access volume.
Volume will be created in one container.
You can declare a directory as a volume only while creating container.
You can’t create volume from existing container.
You can share one volume across any number of containers.
Volume will not be included when you update an image.
You can map volume in two ways:
a. Container to container
b. Host to container

Benefits of Volume:
Decoupling container from storage.
Share volume among different containers.
Attach volume to containers.
On deleting container volume doesn’t delete.

Creating Volume from Dockerfile:
Create a Dockerfile and write
#vi Dockerfile
FROM ubuntu
VOLUME “myvolume”

Then create image from this Dockerfile
#docker build -t myimage

Now create a container from this image and run
# docker run -it --name container1 myimage /bin/bash

Now do ls, you can see myvolume.
Now share volume with another container

Container to container
# docker run -it --name container2 (new) --privileged=true –volumesfrom container1 ubuntu /bin/bash

Now after creating container2, myvolume is visible. Whatever you do in one volume, can see from other volume.
# touch /myvolume/samplefile

# docker start container1
# docker attach container1
# ls /myvolume
You can see sample file here then exit.


Now create volume by using command:
#docker run -it --name container3 -v /volume2 ubuntu /bin/bash
# ls
#cd /volume2
Now create one file cont3file and exit
Now create one more container and share volume2

#docker run -it --name container4 --privileged=true --volumefrom container3 ubuntu /bin/bash

Now you re inside container do ls you can see volume2
Now create one file inside this volume and then check in container3 you can see that file.


Volumes (Host to Container)

Verify files in /home/ec2-user
# docker run -it --name hostcontainer -v /home/ec2-user:/container --privileged=true ubuntu /bin/bash
# cd /container
Do ls, now you can see all files of host machine.
#touch contanerfile (in container) and exit
Now check in EC2 machine you can see this above file.

Some other commands:
#docker volume ls
#docker volume create <volumename>
#docker volume rm <volumename>
#docker volume prune (it removes all unused docker volume)
#docker volume inspect <volumename>
#docker container inspect <containername>


Docker Port Expose:
Login into AWS account, create one linux instance.
Now go to putty -> login as -> ec2-user
#sudo su
# yum update -y
# yum install docker -y# service docker start
# docker run -td --name techserver -p 80:80 ubuntu  // d= detached mode
# docker ps
# docker port techserver o/p- 80/tcp – 0.0.0.0/80
# docker exec -it techserver /bin/bash
# apt-get update
# apt-get install apache2 -y
# cd /var/www/html
# echo “write some msg” > index.html
#service apache2 start
# docker run -td --name myjenkins -p 8080:8080 jenkins

Difference between docker attach and docker exec:
➢ Docker ‘exec’ creates a new process in the container’s environment while docker ‘attach’
just connect the standard input/output of the main process inside the container to
corresponding standard input/output error of current terminal.

➢ Docker ‘exec’ is specifically for running new things in an already started container be it a
shell or some other process.

What is the difference between docker expose and publish:
Basically you have three options:
1. Neither specify expose nor -p
2. Only specify expose
3. Specify expose and -p
1. If you specify neither expose nor -p, the service in the container will only be accessible
from inside the container itself.
2. If you expose a port, the service in the container is not accessible from outside docker but
from inside other docker containers so this is good for inter-container communication.
3. If you expose and -p a port, the service in the container is accessible from anywhere even
outside docker.If you do –p but do not expose docker does an implicit expose. This is because if a port is open to
the public, it is automatically also open to the other docker containers. Hence -p includes expose.

How to push docker image in docker hub:

Go to AWS account – select Amazon linux
Now go to putty – login as – ec2-user
#sudo su
#yum update -y
#yum install docker -y
#service docker start
#docker run -it ubuntu /bin/bash
Now create some files inside container, now create image of this container
#docker commit container1 image1

Now create account in hub.docker.com

Now go to EC2 instance
#docker login
Enter your username and password
Now give tag to your image
#docker tag image1 dockerid/newimage
#docker push dockerid/newimage
Now you can see this image in docker hub account

Now create one instance in another region and pull image from hub
#docker pull dockerid/newimage
To pull private image it will ask password
Run container from pulled image
# docker run -it --name mycon dockerid/newimage /bin/bash

Some important commands:
Show layered architecture of image: # docker image history <Reponame:tag> 
Show details of docker application: # docker image inspect <image_name> 
Stop all running containers: # docker stop $(docker ps -a -q)
Delete all stopped containers: # docker rm $(docker ps -a -q)
Delete all images: docker rmi -f $(docker images -q)

Docker stop vs kill:

#docker stop <container_name>  // docker stop is short form of #docker container stop
it will shut down the application before stop container
you can verify this by 
# docker logs -f <container_name> // -f: follow mode, means it will show continues logs

#docker kill <container_name>
It will immediatly kill the container without shutting down application

Remove all stopped conatiners
# docker container prune 

# docker system <COMMAND>
Commands:
  df          Show docker disk usage # docker system df
  events      Get real time events from the server # docker system events //it will show all events like start, kill, stop etc.
  info        Display system-wide information
  prune       Remove unused data  # docker system prune // it will delete all stopped containers as well as images that have no single containers

To check memory and cpu utilization of a container:
# docker stats <container_id>

To limit memory and cpu usage for a container
# docker run  -td -m 512m --cpu-quota=50000 --name parrot1 <image_id>
 // -m: memory,  cpu-quota :full=100000 half:50000
 
----------------------------------------------------------------------------------------------------------------------------------------- 
 Improve layered caching:
 
FROM python:alpine3.10
WORKDIR /app 
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
ENTRYPOINT ["python", "./launch.py"]

Here we are copying all files in layer one (lauch + requirements) because of this we cant use caching for requirements in subsequent build
if any code change happend in main file (launch.py)

 V/S
 
FROM python:alpine3.10
WORKDIR /app 
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . /app
ENTRYPOINT ["python", "./launch.py"]
 
In second one we will copy and install requirements in first layer then run application in next layer 
So in subsequent build it will use caching for requiremts installation even if any code changes happened in file (ex: changes in lauch.py)
-------------------------------------------------------------------------------------------------------------------------------------------------- 
 CMD vs ENTRYPOINT
 
 CMD python ./launch.py
 #in CMD command line argument can override fixed argument
 EX:docker run -dp 5000:5000 --name=pyhello python-hello ping google.com 
 In this case ping google.com overrides ./launch.py
 
 ENTRYPOINT ["python", "./launch.py"]
 #it will run fixed argument and not allow commandline argument to override fixed argument
 EX:docker run -dp 5000:5000 --name=pyhello python-hello ping google.com 
 it wont allow ping google.com to override ./launch.py
 
 
 Linking two microservices in bridge network (temproary)
 
 docker run -dp 8000:8000 --name=currency-exchange in28min/mmv2-currency-exchange-service:0.0.12-SNAPSHOT
 docker run -dp 8100:8100 --name=currency-conversion --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --link currency-exchange in28min/mmv2-currency-conversion-service:0.0.1-SNAPSHOT

 Creating custom network
# Docker network 
o/p:
Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

# docker network create custom-net
# docker run -dp 8000:8000 --name=currency-exchange --network=custom-net in28min/mmv2-currency-exchange-service:0.0.1-SNAPSHOT
# docker run -dp 8100:8100 --name=currency-conversion --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --network=custom-net in28min/mmv2-currency-conversion-service:0.0.1-SNAPSHOT

Docker compose
-> sudo apt install docker-compose

Create docker compose file
 -> vi docker-compose.yml
          version: '3.7'
          services:
            currency-exchange:
              image: in28min/currency-exchange:0.0.1-RELEASE
              ports:
                - "8000:8000"
              restart: always
              networks:
                - currency-compose-network

            currency-conversion:
              image: in28min/currency-conversion:0.0.1-RELEASE
              ports:
                - "8100:8100"
              restart: always
              environment:
                CURRENCY_EXCHANGE_SERVICE_HOST: http://currency-exchange
              depends_on:
                - currency-exchange
              networks:
                - currency-compose-network

          # Networks to be created to facilitate communication between containers
          networks:
            currency-compose-network:
            
    # save the file and run
    -> docker-compose up 
     It will create network as well as microservice and run it
     or 
    -> docker-compose up -d //it will run in dettached mode
    
     To verify visit:
     http://localhost:8000/currency-exchange/from/USD/to/INR
     http://localhost:8100/currency-conversion/from/EUR/to/INR/quantity/10
     
     -> docker-compose events
     //it will show all events happening while creating container
     
     -> docker-compose down
      //It will remove container as well as network created by docker compose file
      
      -> docker-compose -config 
      //It will validate docker-compose.yml file syntax
      
      -> docker-compose images //show images pulled/used by docker-compose file
      -> docker-compose ps //show running containers
      
      -> docker-compose top
      //It will show top process/services running in a each container
      
      -> docker-compose pause
      -> docker-compose unpause
      -> docker-compose stop 
      -> docker-compose kill
      -> docker-compose start
      
      
