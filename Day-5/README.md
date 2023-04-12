### VOLUME 

- VOLUME is nothing but data by default docker will remove the data whenever you store something in it.
- Docker containers are ephemeral, when you remove the container by default it will delete the data.
- Whatif if you need somedata whenever you remove the container also
- For example if your running database containers. If you remove the mysql container but you should remove the container but should not remove the data because it is user data.
- The requriment is whenever you will recreate the container again it will show same data. For that docker will give the docker volumes.
- Container should not have any file system it can store the data but it uses the host filesystem.


*  ![image-1681107295766.jpg7810461259719627187.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d5f9f9b9-e5c7-4f54-a21e-6d8a9148f31a/image-1681107295766.jpg7810461259719627187.jpg)

- Generally container is running where the docker stores the information is
- 

```bash
cd /var/lib/docker/
cd /overlay2/
```

- Docker will store the data at the location

```bash
cd /var/lib/docker/volumes
```

- First what we needed to do for docker volumes store the data is their is a command

```bash
docker volume create [name-of-volume]
docker volume create nginx
```

- How can i see the volumes by using the command

```bash
docker volume ls
docker volume inspect nginx
```

- Inside nginx a dirctory will created _data it will store the data.

- Finally docker volume is created how can i attached to docker volume to container.

```bash
docker run -d -v nginx:
-p host-port:containerport
-v host-port:containerpart
docker run -d -v nginx:/usr/share/nginx/html -p 80:80 nginx
```

- Inside host you will have a directory for volume. This directory can be mounted with any path inside the container

- /var/lib/docker/volumes/nginx_dat:/usr/share/nginx/html

```bash
/var/lib/docker/volumes/nginx_data:/usr/share/nginx/html
```

### Volume

```bash
FROM ubuntu
RUN mkdir /myvol
RUN echo "hello wold" > /myvol/greeting
VOLUME /myvol
```

- Lets disscuss about mysql image.

- 1st your will create one volume then

```bash
docker volume create mysql-data
docker run -d -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root123 mysql
docker exec -it <contaner id> bash
```

- To login inside the mysql

```bash
mysql -u root -proot123
create database student;
show databases;
```

- Same data can share the multiple volumes also this the biggest avantage o

- You can't loose the data by using.
#
