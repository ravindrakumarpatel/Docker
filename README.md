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

So with the combination of -t and -i we are now attached to the terminal as well as in an interactive mode on the container.


Run - PORT mapping

docker run kodekloud/webapp
* Running on http://0.0.0.0:5000/ (Press Ctrl+C to quit)
If we want user access the application through port 80 on any docker host we could map host port 80 of local host to container port 5000 on the docker container using
the -p parameter in our run

docker run -p 80:5000 kodekloud/webapp

Now the user can access the application by going to the URL http://192.168.1.5:80 
And all traffic on the port 80 on our docker host will get routed to port 5000 inside the docker container.

This way we can run multiple instances of our application and map them to different ports on the docker host or run instances of differenyt application 
on different ports as shown below:

docker run -p 8000:5000 kodekloud/webapp
docker run -p 8001:5000 kodekloud/webapp
docker run -p 8002:5000 kodekloud/webapp


RUN - Volume mapping
Lets now look at how data is persisted in a Docker container. for eg.
let say we were to run a MySql container when databses and tables are created

docker run mysql
here in above case data files are stored in location /var/lib/mysql inside the MySql docker container. Note that the docker container has its own isolated 
file system and any changes to any files happen with in the container.

Lets assume you dump a lot of data into the database. what happens if you were to delete the MySql Container and remove it?

docker stop mysql
docker rm mysql

As soon as you do that the container along with all the data inside it gets blown away, meaning all its data is gone. If we would
like to persists data we would want to map a dierctory outside the container on the docker host to a dierctory inside the container.

docker run -v /opt/datadir:/var/lib/mysql mysql

In this case we created a directory called /opt/datadir and map that to /var/lib/mysql inside the docker container using the -v option
and specifying the directory on the docker host followed by a colon and the directory inside the docker container.
This way when docker container runs, it will implicitly mount the external directory to a folder inside the docker container.
This way all your data will now be stored in the external volume at /opt/datadir and thus will remain even if you delete the 
docker container.

The docker ps command is good enough to get the basic details about container like their names and ID's. But if we would like to see 
additional details about a specific container use the docker insect command.

Inspect Container
docker inspect (container name) or (container id)
eg:
docker inspect blissful_hopper
And it returns all the details of the container in a json formatsuch as the state, mount, configuration data, network settings etc.
Remember to use it when you are required to find details on a container.

Container logs:
How do we see the logs of a container we run in the background?
For example we run a simple web application using the -d parameter and it ran the container in a detached mode.
How do we view the logs which happens to the contents written to the standard out of that container?
Use the docker logs command and specify the docker conatiner id or name like below:

docker logs (container name) or (container id)
eg:
docker logs blissful_hopper

=====================================================================================================================


Advanced docker commands:
docker run ubuntu cat /etc/*release*  (This append command once download ubuntu image will also give details of default latest version say it is 16.04.3)

But what if i want to run another version of this particular Ubuntu Operating system say 17.10, we jsut need to append this tag the name of the image

docker run ubuntu:17.10 cat /etc/*release*  (apended the tag like ubuntu:17:10)

Attach and detach mode:
docker run ubuntu sleep 1500

after hit enter docker container will be running at foreground for next 15 min and we can not come out of the container.
In this case we can either use another terminal to establish another duplicate connection to my docker host.

and with another terminal if we want we can stop the running container which is in sleep mode
docker stop (Container Id)

So if we would like to run it in the background or in a detached mode we could actually specify -d parameter:
docker run -d ubuntu sleep 1500

So -d parameter that is used to run it in the detach mode in the background when it starts.

Now if i would like to attach back to it so i am going to do it for and for that we actually do a docker attach and specify the container Id.
docker attach (Container Id)

And the above command will being docker process conatiner and right in the foreground, back to the same situation and then we can go to 
another terminal to stop the docker container.

=================================================================================================================================



JENKINS:
It is a build system. It is a continuous integration and continuous delivery server. So if we want to just play around the hands on experience 
on it instead of going through the installation instructions and installing a lot of dependencies on my underlying post.
What we would like to do is simply run Jenkins as a container and just play around with it that way.

https://hub.docker.com/_/jenkins

Article on Jenkins Image:

This is an update for the Jenkins image.
In our upcoming demo video, I used a jenkins image which is now deprecated. Instead of that, we have to use jenkins/jenkins.

In the demo video, I used the command:-
docker run jenkins

But as of now, we have to use the following command:-
docker run jenkins/jenkins

So simply if we run jenkins container, it will go out and pull the jenkins images and layers and run the instances of jenkins.

docker run jenkins/jenkins

So as we know Jenkins is a web server so what we are expecting is once we deploy this particular container we are actually expecting 
to go to a web site to a browser  and browse to this jenkins server and access the web UI.
So once the above command gets completed and finished pulling the images, that means we can see its extracted and Jenkins is actually running.

so if we want to reconfirm it we can run below command to check:
docker ps

Now to access the web, this particular application on the wbe UI. One is the terminal IP and another is using by mapping a port to the my docker
host and accessing it using the external IP.

So to access it using the internal IP we need to be inside our docker host.

Now to got browser and eneter the internal IP address in it. SO to find out the internal IP of the docker container run below command and take 
docker container id of Jenkins
docker ps 

Then run docker inspect command folowed by container id and we will see lots of information about docker container status and if we scroll down the
network section we will see the that it is using bridge network and we can see the IP address details as well say it is 172.17.0.2

docker inspect (container id)

Now go back to UI from our host and we have to open browser and enter the IP 172.17.0.2:8080
And then we will notice that we will land actually on the Jenkins page and then we can follow the instruction that is there as it requires 
some user id and password.

SO when we did run the docker run jenkins/jenkins command and after its successfull run in the host it has generated the user id and password
details that we need to use in the web browser.

Now how do we access it externally:
So open a web page and go to IP of our docker host which is 192.168.1.14:8080 and if we try to access the jenkins server using that IP address
we won't be able to access. This is because that particular port or service not listening on the docker host.

Now in order to do that as we saw in the lecture we need to add port mapping.

So we can not a add port mapping while the srevice is running so we have to stop. Check docker ps if its running or not and then stop.

then run below:
docker run -p 8080:8080 jenkins/jenkins

once above command successfully established and if we go back the external browser and run 192.168.1.14:8080 , then we will be able to see 
jenkins page which will requier the admin password again.
Eneter the password and move ahead by following the instructions, no need to install Jenkins and all.


How to use this image
docker run -p 8080:8080 -p 50000:50000 jenkins
This will store the workspace in /var/jenkins_home. All Jenkins data lives in there - including plugins and configuration. You will probably want to make that a persistent volume (recommended):

docker run -p 8080:8080 -p 50000:50000 -v /your/home:/var/jenkins_home jenkins
This will store the jenkins data in /your/home on the host. Ensure that /your/home is accessible by the jenkins user in container (jenkins user - uid 1000) or use -u some_other_user parameter with docker run.

You can also use a volume container:

docker run --name myjenkins -p 8080:8080 -p 50000:50000 -v /var/jenkins_home jenkins
Then myjenkins container has the volume (please do read about docker volume handling to find out more).


==============================================================================================================================================
**How to create your own image**

Before that why would you need to create your own image?
It could either be because you can not find a componenet or a service that you want ti use as a part of you application on
Docker Hub already or you and your team decided that the application youe are developing will be authorized for ease of
shipping and deployment.

In this case, I am going to containerized an application, as simple web application that i have built using the Python flask framework.

What am i containerizing?
First we need to understand what we are containerizing or what application we are creating an image for and how the application is built.

So start by thinking what you might do if you want to deploy application manually.
We write down the steps required in the right order and creating an image for a simple web application.

How to create my own image?
If i were to set it up manually, I would start with  an operating system like Ubuntu then update the source repository using the apt command
, then install dependencies using the apt command, then install python dependecies using pip command, the copy over the source code of my
application to a location like OPPT and then finally run the web server using the flask command.

1 - OS - Unbuntu
2 - Update apt repo
3 - Install dependencies using apt
4 - Install Python dependencies using pip
5 - Copy source code to /opt folder
6 - Run the webserver using 'Flask' command

Now that I have instructions, create a Docker file using these.
Here is a quick overview of the process of creating your own image.

DockerFile:

From Ubuntu
RUN apt -get update && apt-get -y install python
RUN pip install flask flask-mysql
copy ./opt/source-code
ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run











































