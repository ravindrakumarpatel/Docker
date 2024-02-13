# Docker
Docker note - Mumshad in Udemy
www.kodekloud.com

===========================================================
**Objectives**
-What are Cotainers
-What is Docker
-Why do you need it
-What can it do

-Run Docker Containers
-Create a Docker Image
-Networks in Docker
-Docker Compose

-Docker Concepts

-Docker for Windows/Mac

-Docker Swarm

-Docker vs Kubernetes

==========================================================
**Why do you need Docker**
-Compatibility/Dependency
-Long setup time
-Different Dev/Test/Prod environments

**What can it do**
-Containerize Applications
-Run each service with its own dependencies in separate containers

**What are Containers**
Conatiners are completely osolated environments as in they can have their own Process or services, their own network 
interfaces or their own Mounts just like VM except they all share the same OS kernel.
Different types of containers are LXC/LXD/LXCFS. 
Docker utilizes LXC containers, setting up these container environment is very hard as ther are very low level 
and hence Docker offers a high level tools with several powerful funtionalities making it easy for end user like us.

============================================================
**Docker Editions**
1) Community Edition - set of free docker products
2) Eneterprise Edition - certified and supported container platform that comes with enterprise add ons like image management / image security etc come with some price.

==============================================================
**Resources**

https://docs.docker.com/install/linux/docker-ce/ubuntu/

Join our slack channel for support and discussions.

Slack Group URL:

https://kodekloud.com/pages/community

===============================================================
**docker commands**

Run - start a container
docker run nginx

ps - list all running containers
docker ps

docker ps -a (to see all the containers runing or not)

STOP - stop container
docker stop (NAMES)

Remove command - to remove start or exited container permanently
docker rm (NAMES)

images - list images - to see the list of images available in host
docker images

Remove images - to get rid off or delete all the dependent containers to remove image
docker rmi (REPOSITORY Name)

Pull - download an image
docker run (REPOSITORY Name)

to pull the image and not run the container
docker pull (REPOSITORY Name)

Append a command
docker run ubuntu
docker run ubuntu sleep 5

Exec - execute a command
docker ps -a (shows all the running container)
docker exec (NAMES) cat /etc/hosts

Run - attach and detach
docker run (REPOSITORY Name)
docker run -d (REPOSITORY Name) - (container will continue to run in the backend)

attach back to the running container later
docker attach (NAMES/ID of the docker conatiner)

Docker Commands:

docker run centos
Unable to find images 'centos:latest' locally
latest: Pulling from library/centos

docker run -it centos bash

cat /etc/*release*
above command will show the details centos linux os name,version and other details

docker ps
The docker ps command lists all the running containers

docker run centos -d sleep 20
-d used to run the conatiner in the back ground, in above command it will run container in the background once started and sleep for 20 sec

docker stop (NAMES) / (CONTAINER ID)
to stop or force killed any particular docker container

docker rm (NAMES) / (CONTAINER ID)
reclean disk space, also to remove multiple docker cotainer at once we can use 
docker rm NAMES1 NAMES2 NAMES3...

docker rmi 
dicker rm used to remove containers and rmi used to remove container images
docker rmi NAMES

Also note that we need to get rid off first all the containers and then the images refrence to that

docker pull NAMES
docker pulls the images and store it locally, and later we can run it

docker exec (CONTAINER ID) cat etc/*release*
to run a command inside a runnig container first identify the container you want to work with then do a docker exec and provide conatainer id
in above example we are going to look the release file to understand what version of the OS is running
















