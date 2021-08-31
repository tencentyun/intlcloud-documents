## Overview
This document describes how to build and use Docker on a Tencent Cloud CVM instance, and is designed for new CVM developers who are familiar with the Linux operating system.

## Software

This document uses the following software to build the Docker environment:
- Operating system: Linux operating system. This document uses CentOS 7.6 as an example.
>? Docker must be built on a 64-bit operating system with the kernel version 3.10 or later.
>

## Prerequisites
A Linux CVM is required to set up a Docker environment. If you have not purchased a Linux CVM yet, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
>? Docker must be built on a 64-bit operating system with the kernel version 3.10 or later.
>

## Directions

### Installing Docker

1. See [Log into Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436). You can also use other login methods that you are more comfortable with:
 - [Log into Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Logging into Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
2. Run the following commands in sequence to add the yum repository.
```
yum update
```
```
yum install epel-release -y
```
```
yum clean all
```
```
yum list
```
3. Run the following command to install Docker.
```
yum install docker-io -y
```
4. Run the following command to run Docker.
```
systemctl start docker
```
5. Run the following command to check the installation result.
```
docker info
```
If you see the following prompt, it indicates that Docker has been successfully installed.
![](https://main.qcloudimg.com/raw/a848737e9d011f528f66dc54fca61c08.png)


### Using Docker
You can use Docker with the following commands:
- Manage the Docker daemon.
 - Run the Docker daemon.
```
systemctl start docker
```
 - Stop the Docker daemon.
```
systemctl stop docker
```
 - Restart the Docker daemon.
```
systemctl restart docker
```
- Manage images. This document uses the Nginx image of Docker Hub as an example.
```
docker pull nginx 
```
 - Modify image tag to help you identify the image.
```
docker tag docker.io/nginx:latest tencentyun/nginx:v1
```
 - Query existing images.
```
docker images
```
 - Forcibly delete an image.
```
docker rmi -f tencentyun/nginx:v1
```
- Manage containers.
 - Enter a container.
```
docker run -it ImageId /bin/bash
```
Run the `docker images` command to obtain the `ImageId` value.
 - Exit the container. Run the `exit` command to exit the container.
 - Enter a container running in the background.
```
docker exec -it container ID /bin/bash
```
 - Create an image from the container.
```
docker commit <container ID or container name> [<repository name>[:<tag>]]
```
For example:
```
docker commit 1c23456cd7**** tencentyun/nginx:v2
```

### Creating images

1. Run the following command to open the “Dockerfile” file.
```
vim Dockerfile
```
2. Press **i** to switch to edit mode and enter the following content:
```
FROM tencentyun/nginx:v2  #Declare a basic image.
MAINTAINER DTSTACK #Declare the image owner.
RUN mkdir /dtstact #Add the command that needs to be  run before the container starts after the RUN command. Since Dockerfile files can only contain a maximum of 127 lines, we recommend that you write and run the commands in the script.
ENTRYPOINT ping https://cloud.tencent.com/ #The commands that run at startup. The last command must be a frontend command that runs constantly. Otherwise, the container will exit after running all commands.
```
3. Press **Esc** and enter **:wq** to save the file.
4. Run the following command to build an image.
```
docker build -t nginxos:v1 .  #The single dot (.) specifies the path of the Dockerfile and must be included.
```
5. Run the following command to check if the image has been created.
```
docker images
```
6. Run the following commands in sequence to run and check the container.
```
docker run -d nginxos:v1         #Run the container in the background.
docker ps                        #Check the running container.
docker ps -a                     #Check all containers including those that are not running.
docker logs CONTAINER ID/IMAGE   #Check the startup log to troubleshoot the issue based on the container ID or name if you do not see the container in the returned results
```
7. Run the following commands in sequence to create an image.
```
docker commit fb2844b6**** nginxweb:v2 #Add the container ID and the name and version of the new image. after the commit command.
docker images                    #List local images that have been downloaded and created.
```
8. Run the following command to push the image to the remote repository.
The image is pushed to Docker Hub by default. To push the image, log in to Docker, tag and name the image in the following format: `Docker username/image name: tag`.
```
docker login #Enter the username and password of the image registry after running the command
docker tag [image name]:[tag] [username]:[tag]
docker push [username]:[tag]
```
After the image is pushed, you can log in to Docker Hub to view the image.



