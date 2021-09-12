
Avoid re-writing layers
• Avoid mv, chmod in RUN layers
• Remove unnecessary files within the same RUN block
• Use different RUN blocks for distinct tasks for efficient caching of layers

**Running and debugging Containers**

    docker run –-detach \ # Detach terminal
    --rm \ # Remove container on exit
    --env FOO=bar \ # set env variable FOO=var
    --hostname=abhost \ # Set hostname in the container
    --publish 6000:5000\ # Map container port 5000 to 6000 on host
    –name abtest \ # container name (easier than ID)
    myImage:4-1-1 # Image name:tag


    docker ps –a or docker containers ls -a

    docker exec -it web-server /bin/bash
    docker exec web-server ls /etc/nginx

    #one command 
    docker exec <container name> <command>
    
    # interactive
    docker exec -it <container name> <command>



## Docker Basic Commands


| COMMANDS                 | DESCRIPTIONS                                   |
| :----------------------- | :--------------------------------------------- |
| systemctl start docker   | Start Docker service                           |
| systemctl restart docker | Restart Docker service                         |
| systemctl enable docker  | Enable Docker to start at reboot               |
| systemctl status docker  | Check Docker service status                    |
| docker –version          | Check Docker version                           |
| docker info              | Print Docker information in detail             |
| docker system df         | Check disk space being used by your containers |


## Docker Container Commands


| COMMANDS                                                            | DESCRIPTIONS                                                         |
| :------------------------------------------------------------------ | :------------------------------------------------------------------- |
| docker ps Or docker container ls                                    | List only running containers                                         |
| docker ps -a Or docker container ls -a                              | List both running and stopped containers                             |
| docker ps -l                                                        | List the latest created containers                                   |
| docker ps -s                                                        | List all containers by their size                                    |
| docker ps -qa                                                       | List all containers by their ID                                      |
| docker stats                                                        | Show running container stats                                         |
| docker start container-name                                         | Start a container                                                    |
| docker restart container-name                                       | Restart a container                                                  |
| docker stop container-name                                          | Stop a container                                                     |
| docker stop $(docker ps -aq)                                        | Stop all running container                                           |
| docker exec -it container-name /bin/bash                            | SSH into container                                                   |
| docker logs container-name                                          | Check log of a container                                             |
| docker top container-name                                           | Check the running process in a container                             |
| docker inspect -f “{{ .NetworkSettings.IPAddress }}” container-name | Check the IP address of a container                                  |
| docker container rename oldname newname                             | Rename a container                                                   |
| Docker Run Commands                                                 |                                                                      |
| docker container run –name container image                          | Run a container from an image                                        |
| docker container run -d image-name                                  | Run a container in detached mode                                     |
| docker container run -it image-name /bin/bash                       | Run a container in interactive mode                                  |
| docker container run -d -p [host-port]:[container-port] image-name  | Run a container and publish a container port                         |
| docker container run –rm image-name                                 | Run a container that automatically removes a container when it exits |


## Copy a File Between Container and Host



| COMMANDS                                        | DESCRIPTIONS                              |
| :---------------------------------------------- | :---------------------------------------- |
| docker cp container-name:/file/path /host/path  | Copy a file from container to host        |
| docker cp /host/file/path container-name:/path/ | Copy a file from host to container        |
| Docker Image Commands                           |                                           |
| docker images                                   | List all Docker images                    |
| docker tag oldname:tag newname:tag              | Rename an image                           |
| docker search image-name                        | Search available images on the Docker Hub |
| docker history image-name                       | Check command history of any image        |
| docker build -t image-name Dockerfile           | Build an Image from Dockerfile            |
| Docker Registry and Repository                  |                                           |
| docker login                                    | Login to Docker registry                  |
| docker logout                                   | Logout from a Docker registry             |
| docker search image-name                        | Search an image from the Docker registry  |
| docker pull myimage:tag                         | Pull an image from a registry             |
| docker push myrepo/myimage                      | Push an image to registry                 |


## Import and Export Container and Image



| COMMANDS                                     | DESCRIPTIONS                                                         |
| :------------------------------------------- | :------------------------------------------------------------------- |
| docker save -o image.tar image-name          | Export an image to a TAR archive                                     |
| docker load < image.tar                      | Import an image from a TAR archive                                   |
| docker commit container-name image-name      | Create an image from a container                                     |
| docker export container-name > container.tar | Export a container to a TAR archive                                  |
| docker import container-name < container.tar | Import a container from TAR archive                                  |


## Remove Container, Image, Network and Volume 



| COMMANDS                           | DESCRIPTIONS                                                         |
| :--------------------------------- | :------------------------------------------------------------------- |
| docker container rm container-name | Remove a stopped container                                           |
| docker container prune -f          | Remove all stopped container                                         |
| docker rmi image-name              | Remove an unused Docker image                                        |
| docker rmi $(docker images -a -q)  | Remove all unused Docker images                                      |
| docker image prune -a              | Remove all dangling images                                           |
| docker system prune -af            | Remove unused and dangling images, networks, containers, and volumes |
| docker volume rm volume-name       | Remove a Docker volume                                               |
| docker network rm network-name     | Remove a Docker network                                              |