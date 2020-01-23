# Docker

![image](https://user-images.githubusercontent.com/33985509/59151535-0c8d5700-8a35-11e9-8b9a-7959186806b9.png)



# Access given same as root user#

sudo groupadd docker
sudo gpasswd -a $USER docker
sudo systemctl docker restart

# container (if images is there)#

docker run jenkins


# Container(its pulls images and run a new container)

docker run -it jenkins

# to run container in background **

docker run -d jenkins

# to list running container 

docker ps

# to see last container was started 

docker ps -l

# to see the ID of conatiner **

docker ps -q

# to see logs of container (starting 4 letters is enough)

docker logs 8fde



# to see using tail command with conatiner id**
docker logs --tail 6 8fde



# Kill immediately  with conatiner ID
docker kill 8fdebb8a8b95



# Stop with Conatiner ID,if conatiner not stops in 10 sec it kills
docker stop 8fdebb8a8b95




# list runnning container**

docker ps


# list of stopped containers**

docker ps -a


*** Image is collection of files + meta data ***
*** Images are made of layers ***
*** Image is a read only filesystem
***Container is encapsulated set of processes running in a read-write copy of filesystem
*** Docker run starts a conatiner from a given image

# Object -oriented programming

images = classes
Layers = inheritance
Containers = similar to instances

***Image namespace are 3***

Root-like (centos)
User (jpetazzo/clock)
Self hosted (localhost:5000/wordpress)



# For Docker build

We can use th edocker pull image using the Dockerfile
1.Create a directory
2.Create an vi Dockerfile 
3. Insert your fields like below

FROM sonarqube:lts

EXPOSE 9000

:wq!

4. we can keep enhancing these 



# CMD & Entrypoint

two important dockerfile commands 







# For Docker push Request ,create a account in docker hub

docker tag 
docker push 



docker run -d -P jpetazzo/web

-d = runs image in background
-P = to make service reachable from other computers(means publish all)
-t = tag to apply to image



# Manually alloactaion of port numbers 

docker run -t -p 80:8000 jpetazzo/web

-p for publishing the port 
port 80 onlocal host  port 8000 on container



# container IP 

docker inspect conatinerid

or like the below


docker inspect --format '{{ .NetworkSettings.IPAddress }}' 192c8d78516d


docker inspect --format '{{ .NetworkSettings.IPAddress }}' 3138203b37fa


docker run -it -d\
		-v $(pwd):/opt/namer \
		-p 80:9292
		training/namer






# Passwordless SSH between containers

If you need passwordless authentication, consider copying your SSH public key to the container when running it. I don't recommend creating an image with the public key on it, but rather having the file on the host system that has all public keys authorized.

Let's create a file:
#mkdir ~/container-ssh-keys
#vim  ~/container-ssh-keys/authorized_keys
#chmod 0600 ~/container-ssh-keys/authorized_keys

Then add your public SSH key to the file, you can add as many as you want. 
Now when starting the container, map this file to /root/.ssh/authorized_keys on the container, e.g

# docker run --name mycon -it -v $HOME/container-ssh-keys/authorized_keys:/root/.ssh/authorized_keys \
ubuntu:16.04 /bin/bash

You should then be able to ssh from your host system with the private key pair for the 
copied public key without being prompted for the password.
# ssh root@container-ip





# Setup DockerUI - a Web Interface for Docker

Docker maintainers have written an awesome script that can be used to install docker engine in Ubuntu 15.04/14.10/14.04, CentOS 6.x/7, Fedora 22, RHEL 7 and Debian 8.x distributions of linux. 
This script recognizes the distribution of linux installed in our machine, 
then adds the required repository to the filesystem, updates the local repository index and 
finally installs docker engine and required dependencies from it. To install docker engine using that script,
 we'll need to run the following command under root or sudo mode.

# curl -sSL https://get.docker.com/ | sh



# If you would like to use Docker as a non-root user, you should now consider

# adding your user to the "docker" group with something like:
  
  
  sudo groupadd docker
  sudo usermod -aG docker $USER
  
  or 
  sudo usermod -aG docker your-user



docker run -d -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock uifd/ui-for-docker
docker run -d -p 9000:9000 --privileged -v dockerui:/var/run/docker.sock uifd/ui-for-docker

Not working 


https://www.projectatomic.io/blog/2015/08/why-we-dont-let-non-root-users-run-docker-in-centos-fedora-or-rhel/







----------------------------------------------------------------------------------------------------------------------------------------



**Docker**






 | **Application** | **Link** |  **Notes**  | 
------------ |------------ | ------------- 
Docker Engine - Community  (Free Opensource)      | [Reference URL](https://www.docker.com/)  [Reference Docs](https://docs.docker.com/install/)  [Reference Git](https://github.com/portainer/portainer) |  
Portainer (Free Opensource) UI    |    [Access URL]  [Reference Url](https://www.portainer.io/) | 




Install Docker on Ubuntu 18.04

`sudo apt install docker-ce`

or 

`sudo curl -sSL https://get.docker.com/ | sh`


![image](https://user-images.githubusercontent.com/33985509/72986042-9c76ea00-3de7-11ea-8f62-c6cc7709ba35.png)



if we install as `sudo apt install docker` (Don't not work ) it will miss most packages

![image](https://user-images.githubusercontent.com/33985509/72986080-af89ba00-3de7-11ea-89fe-206bf8d3cc9a.png)




Using url to download   `https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/`

wget or curl


amd64 :


`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/containerd.io_1.2.6-3_amd64.deb`    (Optional)

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_19.03.5~3-0~ubuntu-bionic_amd64.deb`

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_19.03.5~3-0~ubuntu-bionic_amd64.deb`

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce_19.03.5~3-0~ubuntu-bionic_amd64.deb`



arm64 :

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/arm64/containerd.io_1.2.6-3_arm64.deb`    (Optional)

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/arm64/docker-ce-cli_19.03.5~3-0~ubuntu-bionic_arm64.deb`

`https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/arm64/docker-ce_19.03.5~3-0~ubuntu-bionic_arm64.deb`



Download the file, and make a note of the path where you saved it

`sudo dpkg -i /path/to/package.deb`




Check Docker Status

`sudo systemctl status docker`

`sudo systemctl start docker`

`sudo systemctl enable docker`



Check Docker Version

`docker --version`

Client Version : 18.09.7

Server Engine Version : 18.09.7



To pull image from Dockerhub (https://hub.docker.com/)

`sudo docker pull [image_name]`


To list images in our local system

`sudo docker images`


command to execute our image 

`sudo docker run -i -t [image]`



Start/Stop/Attach Container


`docker start <CONTAINER_ID> or <CONTAINER_NAME>`


`docker stop <CONTAINER_ID> or <CONTAINER_NAME>`


`docker attach <CONTAINER_ID> or <CONTAINER_NAME>`




Before running container we need to provide any of the below flags

**Docker’s Restart Policy**


1.no -  policy is the default restart policy and simply does not restart a container under any circumstance


2.on-failure -

```
Example :sudo docker run -d --name container_name --restart on-failure:5 image:latest

```

3.unless-stopped

```
Example : sudo docker run -d --name container_name --restart unless-stopped image:latest

```

4.always - If we wanted the container to be restarted regardless of the exit code

```
Example : sudo docker run -d --name container_name --restart always image:latest

```


Adding a restart policy to a container that was already created


`docker update --restart=always <CONTAINER_ID> or <CONTAINER_NAME>`




**Access using below link**

[Portainer](http://cis:9000/#/dashboard)


Username: admin

Password : password





Portainer is a lightweight management UI which allows you to easily manage your different Docker environments 

we choose local ,can be used to manage remote environment and portainer agent


![image](/uploads/20874e2572f982232b40744028c4f6a0/image.png)






# Docker in Docker #

sudo apt-get install docker-ce (does not work)

Following the below process

Update Local Database

`sudo apt-get update`

Download Dependencies

`sudo apt-get install apt-transport-https ca-certificates curl software-properties-common`


```
apt-transport-https: Allows the package manager to transfer files and data over https

ca-certificates: Allows the system (and web browser) to check security certificates

curl: This is a tool for transferring data

software-properties-common: Adds scripts for managing software

```

To ensure that the software you’re installing is authentic

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –`

 Install the Docker Repository

`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu  $(lsb_release -cs)  stable" `


update repo

`sudo apt-get update`

Install Latest Version of Docker

`sudo apt-get install docker-ce`



**Commands:**


Command | Comments
------- | --------
`sudo docker ps`
`sudo docker ps -a`
`docker run -itd --name portainer -h portainer -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart on-failure:2 portainer/portainer:latest`
`docker rm $(docker ps -a -f status=exited -q)`
`docker rmi $(docker images -a -q)`
`docker volume rm $(docker volume ls -f dangling=true -q)`



docker run -itd --name docker0 -h docker0 ubuntu:18.04

apt update 

apt install sudo vim apt-utils net-utils nmap   

sudo curl -sSL https://get.docker.com/ | sh

service docker start (it won't start properly)

sudo dockerd


![image](https://user-images.githubusercontent.com/33985509/72986134-cb8d5b80-3de7-11ea-9f8b-f56619ac6e9a.png)


`docker run -itd --name docker01 -h docker01 --privileged ubuntu:18.04`


Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?


service docker start

service docker stop

service docker restart

service docker status


or 

we can run as below

`docker run -itd --name docker02 -h docker02 --privileged -v /var/run/docker.sock:/var/run/docker.sock ubuntu:18.04`
