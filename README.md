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


Run - tag
docker run redis
it will display latest Redis version say 5.0.5

But if we wnat to run anaother version of redis like an older version say photo zero, then specify a version separated by a colon
docker run redis:4.0 
here redis:4.0 is call as a Tag and in this case docker will pull the images of 4.0 version of Redis and run that

Note: So if do not specify any tags as in the first command (docker run redis), docker will considered the default tag to be latest.
Latest is a tag associated to the latest version of that software which is governed by the authors of that software.


RUN - STDIN
simple prompt application that when runs ask for name and on entering name prints welcome message.
If i were to dockeries this application and run it as a docker container like this, it would not wait from the prompt

~/prompt-application/$ ./app.sh
Welcome! Please enter your name: Ravindra

Hello and welcome Ravindra!

It just prints whatever the application is supposed to print on the standard out
docker run kodekloud/simple-prompt-docker

Hello and welcome ! 

That is because the docker container does not listen to a standard input, even though are attached to its console. It is not able to read any input from you.
It does not have a terminal to read inputs from. It runs in non a interactive mode.

If we would like to provide an input, we must map the standarad input of our host to the docker container using the -i parameter.
-i parameter is used for interactive mode, and when we input our name, it prints the expected output.

docker run -i kodekloud/simple-prompt-docker

Ravindra (when input our name)
Hello and Welcome Ravindra!

But there is something still missing from this. The prompt, when we ran the app, at first it asked us for our name.
But when dockerised that prompt is missing, even though it seems to have accepted our input.
That is because the application prompt on the terminal and we have not attached to the containers terminal.

For this use the -t option as well:
docker run -it kodekloud/simple-prompt-docker

Here -t stands for a pseudo terminal and when run below command it will ask for enetering the name and display then welcome message:
docker run -it kodekloud/simple-prompt-docker

Welcome! Please enter your name: Ravindra
Hello and Welcome Ravindra!

So with the combination of -i and -t we are now attached to the terminal as well as in an interactive mode on the container.





















