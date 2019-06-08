# docker

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
