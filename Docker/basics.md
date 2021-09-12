**TOPICS**

1. Docker image creation
2. Docker tagging
3. Docker port mapping
4. Docker container configuration

**Install Docker** (root permission)

    sudo yum -y install docker
    sudo systemctl start docker
    sudo docker info
    sudo systemctl restart docker

Using Docker without Root Permission on Linux

    docker info

Verify the docker group exists by searching for it in the groups file:

    grep docker /etc/group

If you don't see a line beginning with "docker:", you will need to add the group yourself by entering:

    sudo groupadd docker
 
Add your user to the docker group:

    sudo gpasswd -a $USER docker

The groups of the currently logged in user is cached, you can verify this by entering:
     groups


You can login again to have your groups updated by entering:

    newgrp docker

Now you will have docker in your list of groups if you enter 
    groups

Note: It is convenient to not have to terminate your current ssh session by using newgrp, but terminating the ssh session and logging in again will work just as well.

Verify that your user can successfully issue Docker commands by entering:

    docker info

Note: if you don't see the system-wide Docker information, you may need to restart the Docker daemon by entering sudo systemctl restart docker.

**HELP**

    docker --help
    docker command-name [options] 
    docker management-group command-name [options]

e.g 

    docker system --help
    docker image --help
    docker container --help

**RUN Docker Applictions**

    docker run --name web-server -d -p 8080:80 nginx:1.12

This time you specified the tag 1.12 indicating you want version 1.12 of nginx instead of the default latest version. There are three Pull complete messages this time, indicating the image has three layers. The last line is the id of the running container. The meanings of the command options are:

--name container_name: Label the container container_name. In the command above, the container is labeled web-server. This is much more manageable than the id, 31f2b6715... in the output above.

-d: Detach the container by running it in the background and print its container id. Without this, the shell would be attached to the running container command and you wouldn't have the shell returned to you to enter more commands.

-p host_port:container_port: Publish the container's port number container_port to the host's port number host_port. This connects the host's port 8080 to the container port 80 (http) in the nginx command.

To list all running containers, enter:

    docker ps

To list of all running and stopped containers:

    docker ps -a

To stop

    docker stop web-server

To start running the command in the web-server container again, enter

    docker start web-server

This is different from re-running the original docker run command, which would make a second container running the same command instead of using the stopped container.

 To see the container's output messages, enter

    docker logs web-server

 You can run other commands in a running container. For example, to get a bash shell in the container enter

    docker exec -it web-server /bin/bash

This indicates you are at a shell prompt in the container using the root container user. The -it options tell Docker to handle your keyboard events in the container. Enter some commands to inspect the container environment, such as ls and cat /etc/nginx/nginx.conf. When finished, enter exit to return to the VM ssh shell. Your shell prompt should change to confirm you are no longer in the container bash shell.

You were able to connect to a bash shell because the nginx image has a Debian Linux layer which includes bash. Not all images will include bash, but exec can be used to run any supported command in the container.

    docker exec web-server ls /etc/nginx

This runs the ls command and returns to the ssh shell prompt without using a container shell to execute the command. What commands are supported depends on the layers in the container's image. Up until now you have used two images but don't know how to find more.


Search for an image that you don't know the exact name of, say an image for Microsoft .NET Core, by entering:

    docker search "Microsoft .NET Core"

**Creating Your First Docker Image**

Preperation:

    sudo yum -y install git
    git clone https://github.com/cloudacademy/flask-content-advisor.git
    cd flask-content-advisor
    vi Dockerfile

Enter the following in the file:

    # Python v3 base layer
    FROM python:3

    # Set the working directory in the image's file system
    WORKDIR /usr/src/app

    # Copy everything in the host working directory to the container's directory
    COPY . .

    # Install code dependencies in requirements.txt
    RUN pip install --no-cache-dir -r requirements.txt

    # Indicate that the server will be listening on port 5000
    EXPOSE 5000

    # Set the default command to run the app
    CMD [ "python", "./src/app.py" ]


Build the image from the Dockerfile:

    docker build -t flask-content-advisor:latest .


The -t tells Docker to tag the image with the name flask-content-advisor and tag latest. The . at the end tells Docker to look for a Dockerfile in the current directory. Docker will report what it's doing to build the image. Each instruction has its own step. Steps one and four take longer than the others. Step one needs to pull several layers for the Python 3 base layer image and Step four downloads code dependencies for the Flask web application framework. Notice that each Step ends with a notice that an intermediate container was removed. Because layers are read-only, Docker needs to create a container for each instruction. When the instruction is complete, Docker commits it to a layer in the image and discards the container.


Now you can run a container using the image you just built:

    docker run --name advisor -p 80:5000 flask-content-advisor