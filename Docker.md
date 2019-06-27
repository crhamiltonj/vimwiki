# Docker

## Installation
* Direct - For linux, windows server 2016
* Docker for Mac/Windows -- Creates a Linux VM to run Docker
* Docker for AWS/Azure/Google

## Editions
* Community
* Enterprise

## Releases
* Stable 
* Edge

## Installing docker
* Windows 10 Pro or Enterprise
  * Install Docker for Windows -- Needs HyperV and Powershell
* Windows 7, 8 or 10 Home Edition
  * Install Docker Toolbox
* MacOS
  * Install Docker for Mac
* Linux
  * use the following command line:
    `curl -sSL https://get.docker.com/ | sh`
    
## Important Docker Commands
* docker version
  `docker version`
  returns the versions of the docker client and server
* docker info
  `docker info`
  gives more details about the docker setup.
* Runnning Docker Commands
  Docker commands run in the format
  `docker <management_commanmd> <sub_command> (options)`
  
## Images vs Containers
* Image - The binaries and libraries of the application that we want to run
* Container - The instance of an image running as a process on the host
* Registry - A place either local or on hub.docker.com that stores images
 
## Getting Inside a Container
* `docker container run -it <containername> <command>` -- start a new container interactively
* `docker container exec -it <containername> <command>` -- run an addtional command inside an existing container

## Docker Networks
* Show networks : `docker network ls`
* Inspect a network : `docker network inspect <network_name>`
* Create a network : `docker network create --driver <driver_name> <network_name>`
* Attach a network to a container : `docker network connect <network_name> <container_name>`
* Detach a network from container : `docker network disconnect <network_name> <container_name>`
 
## DNS on Docker
* Containers shouldn't rely on IP Addresses for inter-communication
* DNS for friendly(container) names is built-in if you use custom networks (`docker network create`)
* 
