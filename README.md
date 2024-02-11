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

ps - list all containers
docker ps


