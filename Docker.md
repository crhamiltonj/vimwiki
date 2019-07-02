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

## Sending images to docker hub

Images have to be tagged properly

* Tagging an image -- `docker image tag <SOURCE_IMAGE>[:<TAG>] TARGET_IMAGE[:<TAG>]`
* Pushing and image -- `docker image push <REPO_NAME>/<IMAGE_NAME>:<TAG>`

## Dockerfile

The Dockerfile is a recipe for creating an image.

* FROM -- specifies a base image, usually some minimal to be built on by the rest of the Dockerfile
* ENV -- sets environment variables
* RUN -- commands to run inside the container at build time
* EXPOSE -- Specifies ports that can be exposed from the container to the virtual network
  This is a space separated list
* CMD -- The command that is run when the container is launched
* WORKDIR - set the current folder inside the container
* COPY -- copies the file from the host to the container
Format: COPY <HOST_FILE> <CONTAINER_FILE>

### Docker Build

* Format: `docker image build -t <tagname> .`

### Pruning Images

* `docker image prune` -- cleans up dangling images
* `docker system prune` -- cleans up everything
* `docker image prune -a` -- cleans all images not being used
* `docker system df` show space images are using

## Container Lifetime & Persistent Data

* Containers are immutable and ephemeral (Disposable)
* immutable infrastructure: only redeploy containers, never modify
* Volumes and Bind Mounts
  * Volumes create a special location outside of the container filesystem
  * Bind Mounts link container path to path on the host

### Volumes

* `docker volume ls` -- list the volumes created by containers or manually
* `docker volume rm <CONTAINER_ID>` -- remove a container
* `docker volume inspect` -- display detailed information on one or more volumes
* `docker volume create` -- manually create a volume to specify drivers or other options
* `docker volume prune` -- remove unused volumes

### Bind Mounts
Maps a host file directory to a container file or directory. It cannot be specified in a Dockerfile, must be specified at container run.

* `docker container run -v <HOST_PATH>:<CONTAINER_PATH> ...`

## Docker Compose

### Docker Compose Features 

* Configures relationships between containers
* Stores docker run setting in an easy to read file
* allow one liner developement environment startups

### Docker Compose Parts

Docker compose is created from two parts

1. YAML file that describes:
  
  * containers
  * networks
  * volumes

2. docker-compose used for local dev and test automation
  
#### Sample docker-compose.yml

```yaml
version: '2'

# same as 
# docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve

services:
  jekyll:
    image: bretfisher/jekyll-serve
    volumes:
      - .:/site
    ports:
      - '80:4000'
```
### Docker Compose CLI
Used for local development and testing

* `docker-compose up` -- sets up volumes and networks and starts all containers
* `docker-compose down` -- stops all containers and removes containers/volumes and networks

## Docker Swarm

<<<<<<< Updated upstream
Swarm brings different hosts or nodes into a single operating unit. You can now orchestrate how the nodes interoperate. 

There are two types of nodes:
* managers -- contains all the information needed to be an authority in a swarm 
* workers -- Can respond to requests from manager nodes

Control Plane -- How orders are sent around the swarm between managers and workers

### Standard commands
* `docker swarm` -- Initializes swarm and sets the host it is run on as manager or allows another host to join an existing swarm. 
* `docker node` -- Used for bringing servers in and out of the swarm and promoting and demoting managers and workers
* `docker service` -- Replaces the docker run command for swarms/cluster. starts containers in a swarm.
* `docker stack`
* `docker secret`

### Overlay Multi-Host Networking
* Just choose `--driver overlay` when creating the network
* Only for container-to-container traffic
* Optional IPSec encryption
* Each service can be connected to multiple networks

=======
>>>>>>> Stashed changes
