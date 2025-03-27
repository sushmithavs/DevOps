DOCKER - The power of Containerization

1)Why use Docker?

Developers often say, “It works on my machine but not on the server!”.
In a project when a team is working on
Different environments
(Windows, Linux, Mac)
they may have different software versions
that causes compatibility issues.

Containers package everything
(code, libraries, dependencies) together,
so the application runs the same way everywhere.

2)What is Docker?

Docker is a platform for developing, shipping, and running applications.
It packages and runs an application in a
loosely isolated environment called a container.

3)What is the Difference between Virtual Machine and Docker?

Vitual Machine’s and Docker are used to create isolated environments enabling the application to work anywhere without any compatibility issues

OS: VM’s are heavy because each VM runs full OS
Performance: Therefore it’s performance is slow.
Resource usage : Needs RAM & CPU for each VM. So Resource usage is high.
Isolation : Strong isolation because VM’s are fully independent
Scalability : Difficult to scale.
Usecase : It is best for running different OS on same machine

Docker runs on the host OS and shares the kernel while keeping applications isolated.
OS: Containers share the host OS, making them lightweight.
Resource usage : low
Isolation : Isolated but Shares the same OS kernel
Scalability : Easy to scale.
Usecase : Best for running multiple instances of applications efficiently.

DOCKER COMPONENTS:

Docker Engine : It helps in creating, running and managing containers on your system.
Docker Hub: A cloud repository for finding and sharing container images.
Docker File : A script containing instructions to build a Docker image.
Docker Image : A blueprint for creating a container. It contains the application code, libraries and dependencies.
Container : A running instance of an image.

**

STEPS TO BE FOLLOWED IN DOCKER**

1)Install Docker – Install Docker Desktop from docker.com
2) Image Creation:
Docker Pull - Downloads existing image from dockerhub docker pull <image-name>
Docker Build is used to create a new Docker image from a Dockerfile.
docker build -t < image-name > .
3)Run a Container – Creates a container from image docker run -d -p 8080:80 nginx
4)Check running Containers
docker ps
5)Stop a Container -
docker stop <container_id>
6) Remove a Container -- docker rm <container_id>

DOCKER COMMANDS

docker --version - Displays Docker version

IMAGES docker pull <image-name> - Downloads existing image from dockerhub
docker build -t < image-name > . - Create a new Docker image from a Dockerfile.
docker rmi <image_id> - Remove an image
docker tag <image_id> <repo_name>:<tag> - Tag an image for pushing to a registry
docker push <repo_name>:<tag> - - Push an image to Docker Hub
CONTAINER docker run <image_name> - Create and start a container
docker ps - Displays all the running containers and images
docker ps -a - Displays all containers including the history / hidden containers
docker run -d <image_name> - Run a container in the background (detached mode)
docker run -it <image_name> /bin/bash - Run a container in interactive mode
docker stop <container_id> - Stop a running container
docker start <container_id> - Start a stopped container
docker restart <container_id> - Restart a container
docker rm <container_id> - Removes a stopped container
docker logs <container_id> - Show logs of a container
docker inspect <container_id> - Get detailed info about a container
docker exec -it <container_id> bash - Access a running container’s shell
[if !supportLineBreakNewLine]
[endif]

DOCKER FILE
1)Base image
2) Set the working directory inside the container
3) Copy application files into the container
4) Install dependencies
5) Expose a port for the application
6)Command to run the application

DOCKER FILE for Node.js App
# Use an official Node.js runtime as base image
FROM node:18

# Set the working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json .
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose the port
EXPOSE 3000

# Start the application
CMD ["node", "server.js"]
[if !supportLineBreakNewLine]
[endif]

DOCKER VOLUME : To persist the data even if container is removed as data is stored in database docker volume create <volume-name> - Create a volume
docker volume ls - List all volumes
Persistent Storage:
1)docker volume create my_volume
2) Docker run volumes syntax : docker run -v <host_path>:<container_path> <image_name>docker run -d -v my_volume:/app/data myapp
ex:docker run -v <volume-name> :/var/lib/mysql mysql

docker volume inspect <volume_name> - Get volume details
docker volume ls - List all volumes
docker volume rm my_volume - Remove a volume

STORAGE DRIVER : Manages how container data is stored and accessed.
Below are the main storage drivers.
1)AUFs – Legacy systems -Supports multiple layers but outdated
2)ZFS - Enterprise storage solutions - High performance with snapshots and replication
3)BTRFS – Systems that use BTRFS filesystems - Uses block devices for storage
4)Device mapper - Red Hat - Uses block devices for storage
5)Overlay2 – Linux - Efficient, supports multiple layers, better performance
6)Windows filter - Windows filter - Default driver for Windows containers
Docker automatically use the storage driver according to the OS.
Commands:
docker info | grep "Storage Driver" - display the storage driver used by Docker

[if !supportLineBreakNewLine]
[endif]

DOCKER NETWORK : allows containers to communicate with each other & with external networks.
Types:
1)Bridge : Bridge is a Default network that is used for container-to-container communication.
syntax : docker network create my_network
2)Host : Removes network isolation and makes the container use the host’s network
syntax : docker run --network=host my_image
3) none : Disables networking for the containersyntax : docker run --network=none my_imageCommands:docker network ls - List all networks
docker network create <network_name> - Create a new networkdocker network inspect <network_name> - Get network details
docker network connect <network_name> <container_name> - Connect a container to a network
docker network disconnect <network_name> <container_name> - Disconnect container from a n/w
docker network rm <network_name> - Remove a network

DOCKER COMPOSE : define and run multi-container applications Commands:docker-compose up - Start services defined in docker-compose.yml
docker-compose up -d - Start services in detached mode
docker-compose down - Stop and remove containers defined in docker-compose.yml
docker-compose ps - List running servicesdocker-compose logs - Show logs of services

DOCKER SYSTEM CLEANUP : Commands:docker system prune - Remove all unused containers, networks, images, and volumesdocker image prune - Remove unused imagesdocker container prune - Remove stopped containerdocker volume prune - Remove unused volumesdocker network prune - Remove unused networks

DOCKER REGISTRY : It is a storage system for Docker images.
It allows to push, pull, and manage container images.
ex: Docker Hub, Amazon ECR, Google Artifact Registry, Azure Container Registry (ACR), Harbor
docker login - Login to Docker Hubdocker tag <image_id> <username>/<repo_name>:<tag> - Tag an image before pushing
docker push <username>/<repo_name>:<tag> - Push an image to Docker Hub
docker logout - Logout from Docker Hub

*********************************************************************************g