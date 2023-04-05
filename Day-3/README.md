- Recap of previous sessions
- Create one ec2 instance and then connet to putty
1. Created security group
2. Created ec2 instance
3. Connted to putty
4. Install docker on that
5. Practice docker commands
6. Understand dockerhub
# We need to build our own images.
- Dockerfile
- Base os = ubuntu, centos, almalinux
    - Nginx = debian, installed nginx for you
- Image = static file
- Container is a running instance of image.
- Create one ec2 instance and then connet to putty. Install docker on that.
- Dockerfile - FROM, RUN, CMD

### LABEL

- LABEL instruction is useful to give some metadata information.
- Labels or tags both are same are the key value pairs that will be very useful to filter the information from thousands and lakhs of records.
- 
```bash
FROM almalinux
LABEL AUTHOR="CHAKRADHAR"\
      COURSE="DOCKER"\
      DURATION="25 HOURS"
```
If we want to put multiple layers used  “\”
Now push the code to github and clone to ec2 instance while docker is running by using the command.

Or you can give
```bash
docker build -t label:v1 .
```
```bash
docker build -t docker.io/chakradhar933/label:v1 .
```
If you inspect this image
```bash
docker inspect <image id>
```
- How this labels are usefull becuse when you are run docker images your are getting 2 images now.

- for example if you have 2 thousand images in your server how can i filter those images?

- That is based on the labels by using the command
```bash
docker images --filter "label=AUTHOR=CHAKRADHAR"
```
- How to docker images by using label?

Docker images --

### EXPOSE

- Next instrustion is EXPOSE

- Expose instruction is usefull to tell the users of the image about the ports and protocols image/container is opening. It will not have any functionality it used only to tell the information.
- How can you know whether the nginx is opening port number 80 or not what is the port is opening?
- Ans : you will use EXPOSE.
- 
```bash
FROM almalinux
EXPOSE 8080/tcp
```
Now push
```bash
docker build -t expose:v1 .
```
- Now inspect the changes
```bash
docker inspect <image id>
```
To check the port in running container by using command
```bash
sudo docker run expose:v1 sleep 20
```
- Now check
```bash
sudo docker ps
```
### ENV
- ENV is the instruction to provide environment variables for image and container.
- For example if are developing an application if want to connect the database if don't hard code inside the code. You always refers through environment variables.
- 

```bash
FROM almalinux
ENV AUTHOR="CHAKRADHAR"\
    DURATION="25 HOURS"\
    COURSE="DOCKER"
```

Now run in docker

```bash
docker build -t env:v1 .
docker inspect <container id>
docker run env:v1 env

```

To overwrite the environment variables at  run time by using the command

```bash
docker run -e DURATION=30HOURS env:v1 env
```

# COPY

- COPY instruction is useful to copy the files from local to image.
- If want to copy the your website to docker container how you will do?
- Ans: that is using copy command
- 

```bash
FROM almalinux:8
#RUN yum install epel-release -y
RUN yum install nginx -y
RUN rm -rf /usr/share/nginx/html/index.html
COPY vi /usr/share/nginx/html/
CMD ["nginx""-g","daemon off;"]
```

Copy the website inside the COPY directory.

Now

```bash
docker build -t copy:v1.
docker run -d -p 8080:80 copy:v1
```

Now push docker image to docker hub

```bash
docker tag copy:v1 chakradhar933copy:v1
docker push
```

Now you can download the container in the any number of instances sucessfully.

### ADD

Next instruction should be ADD. ADD is same as COPY. It is usefull to copy files from local to container. But it has 2 extra features or capabilities

1. ADD can dowload the file directly from the internet to the container.
2. ADD can untar/unzip the file directly into the container.
```bash
FROM almalinux
ADD <url>/tmp/
ADD
```
- Now push to docker
```bash
docker run -it add:v1 bash
```
- What is the  diffrecence between COPY and ADD ?
- Ans:COPY and ADD both are almost same.