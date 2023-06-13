### Docker installation
                                             
We are using Amazon Linux 2 OS for this. For reference

```
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-container-image.html#create-container-image-install-docker
```
### Connect EC2 instance in AWS

* Create a security group that can allow all IP to all ports. Create inbound and outbound both.
* Launch an EC2 instance with AWS Linux 2 and create key pair in ppk format
* We are going to use Putty and Super putty to connect our instances. You can use any SSH client to connect.
* to connect any instance you need to provide
    * IP
    * Username
    * Password/private key
    * Port (SSH by default takes port number 22)

### Install Docker in AWS Linux 2

* Update OS packages.
```
sudo yum update -y
```

* Install Docker
```
sudo amazon-linux-extras install docker
```

* Start Docker.

```
sudo service docker start
```

* Enable it

```
sudo systemctl enable docker
```

* Add user to docker group

```
sudo usermod -a -G docker ec2-user
```

Just logout and login again to run docker commands with normal user.


* Docker Image : Docker image is a file used to excute the code in a docker container.
how to create the docker image by suing the command
```
docker create <image name>:version
```
```
docker create tomact
```
* To check the docker images by using the command
```
docker images
```
now image is created copy the image id.
* Docker container : Docker container is a running instance of docker image.
* container is a mini server.
To create the container by using the command.
```
docker create <image id>
```
* copy the container id and start the conatiner.
* To check the running containers by using the command.
```
docker ps
```
To check the all the container
```
docker ps -a
```
* To start the conatiner  
```
docker start <container id>
```
* To stop the container
```
docker stop <container id>
* To pull the images from Docker hub dirctly by using the command.
```
docker pull <image name>:version
```
* Docker run  : Docker pull + create + Start.
```
docker run -d nginx
```
* d : detach mode
* p : To attach the port maping to conatiner.
```
docker run -d -p <host port>:<container port> <image name>
docker run -d -p 80:80 nginx
```
* To delete the image 
```
docker rmi -f <container id>
```
* To delete the container.
```
docker rm -f <container id>
```
To login inside the container
```
docker exec -it <container id> bash
```
* ctrl+d to come out of the container.


