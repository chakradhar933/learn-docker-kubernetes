# Previous session recap

- Create one ec2 instance and connet to the instance.
- Install docker in ec2 instance.
- Create a docker container by using command
- 
- Our web server is ready.
- Nginx is not a Os. Container is running version of image.

```bash
docker run -d -p 8080:80 nginx

```

- Image is a static file.
- Ubuntu os is a image. It run into any number of laptops.
- Docker image is a static file it can run any number of containers.
- Image = base os = bareminimum os
- Ontop of base os you can install packages+ softwares.
- To login inside the docker container
- 

```bash
docker exec -it <container id> bash
```

- To see which os is running inside the container
- 

```bash
cat /etc/*release
```

- Nginx = debian os + nginx server installed.
- Copy a webwebsite or create a file inside the nginx html location then we use this container as a website.
- For any docker image must have os.
- Create a file inside the nginx html location.
- For any docker image Os is must.
- Aws linux2 = centos= almalinux= redhat. Same for all.
- Now we will for alma linux for our containers versions.
- Another version we can use
- 

```bash
docker pull nginx:alpine
```

Nginx Alpine is very thin. It is a bare minimum.

```bash
docker pull alpine
```

It has very thin..

To see the default command which will give inginx by using command

We can use out practices almalinux is uses.

```bash
docker run almalinux
```

By using this os to ping [google.com](http://google.com) for 5 times by using the command.

```bash
docker run almalinux ping -c 5 google.com
```

```bash
docker ps --no-trunc
```

Container will de do the job whatever your are giving.

- If you want to container to keep alone it should run a command for infinite times.
- Now going inside the almalinux container by using the command
- 

Inside this  it will not have anything just install and run expectily.

```bash
docker run -it almalinux bash
```

- To install ps command inside the almalinux by using the command

```bash
yum install procps -y
```

Containers have a bare minumum os it don't have unnecessary data if we want you can install it.

- To install clear command in almalinux by using the command

```bash
yum install ncurses -y
```

- Now install nginx in almalinux.

```bash
yum install inginx -y
```

To run in the inginx forground by using the commands

```bash
nginx -g 'daemon off;'
```

### It stick to the session this is what nginx company do it in background whenever they relase in your container.

Ctr+d or exit is the commands to leave the inside the container.

Based upon your business requrement take it and use it.

### Our requriment is to be host a website, you need http server.

* Now we can use nginx as a webserver.

* Then goto the file

*  Now if you want to host inside the container by using simple steps
*  Login in nginx container

```bash
docker exec -it <container id> bash
```

```bash
cd /usr/share/nginx/html

```

Now copy paste our website

```bash
echo "hello docker " > hello.html
```

### How can you create your own docker images?

Ans: For this purpose we are used dockerfile.

 ### **Dockerfiles** :

*  Dockerfile is a declaritive way of creating our own images. Docker will give us some synatax to create our own images.
*  File name should be docker file.

## How to build image from Dockerfile :

- -t is tagging..

```bash
docker build -t[docker-hub-url]/[your-name]/[image-name]:version .
```

### 1st instruction is **From.**
### FROM:
* From should be the 1st instruction in your Dockerfile.
* Filename should be **Dockerfile**.
* In this file we need to write what you want docker will create it.
* Dockerfile: 1st instruction should be FROM  We can use baseOS = almalinux

```bash
FROM almalinux

```

### Now create one repository on github.

* Name : dockerfiles

* Description : this project is to develop ans learn how to buid and push our own images.

* Create repository sucessfully.

### Now How to build image from Dockerfile by using command

```bash
docker build -t docker.io/chakradhar933/chakri/from:v1.
```

By using the command

### **How to push image to DockerHub :**

```bash
docker push [dockerhub url]/[your name]/[image name]:version
```

```bash
docker push chakri/from:v1
```

Now access denied and login to dockerhub in command line then try it push success.

Now you can see at dockerhub and anyone can use this image.

### RUN :

- RUN instruction
- RUN instruction we are to used to install the softwares, packeges and other tasks. It runs at the time of image building.
- Now create one folder : RUN
- Inside craate one file : Dockerfile
- Dockerfile
- 

```bash
FROM almalinux
RUN yum install nginx -y
```

- Then push to github and then run at the server by using the command
- 

```bash
docker run -t <image name>/run:version.
```

```bash
docker push <image name>:version
```

```bash
docker run -t chakradhar933/run:v1.
```

Now check the images by using the command

```bash
docker images 
```

Then push to docker docker hub

```bash
docker push chakradhar933/run:v1
```

### CMD Instruction :

- CMD is the instruction which runs the docker container. It should run foreground and it should run infinite times.
- Create one folder : CMD
- File : Dockerfile
- 
### CMD is the instruction that runs the container.

```bash
FROM almalinux
RUN yum install nginx -y
CMD ["nginx","-g","daemon off;"]
#CMD["sleep","20"] there should be only one cmd instruction. if we give multiple cmd the last one will be conside
```

### 1. What is the difference between RUN and CMD?
- [ ]  RUN command will excute at the time of image creation.
- [ ]  CMD command will excute at the time of running container creation.

Now push to github and clone to docker server.

```bash
git pull

```

Now build the image and run the container.

```bash
docker build -t chakradhar933/cmd:v1 .
```

In this image and container are created successfully.

Now check the image is created or not by using the command.

```bash
docker images

```

Now run the container by using the command

```bash
docker run -d -p 80:80 chakradhar933/cmd:v1
```

-d - is used to run background.

Now container is running successfully.

- Command in background is “nginx  -g deamon off”  like how nginx will build its own container we are also build own nginx container.
- Now login into container by using the command
- 

```bash
docker exec -it container id bash
```

```bash
cd /usr/share/nginx/html
echo "hello world" > hello.html
```

### To delete the all containers by using the command

```bash
docker ps -a -q 
```

### It will give all the container ids.

### Now to delete all containers by using the command

```bash
docker rm -f 'docker ps -a -q'
```

```bash
docker build -t 
```