### Roboshop-project
- Roboshop is the micro-service application used by ibm internal research projects.
- Thier is a web container [frontend] user access the web. This frontend will redirected to multliple micro-services like user, cart, catalogue, shipping, payment, dispatch etc.
- Now take the project from the github and clone to our local repository for reference.
- Now create out own repository name : **Roboshop-project D-K**
- Copy the web content from the reference project and put into our folder.
- 

## Roboshop-project-D-K

1. Web(frontend)
- Copy the static file in web
- Goto Dockerfile and create our own Dockerfile.
- 

```bash
FROM nginx
RUN rm-rf /usr/share/nginx/html/index.html
ADD static /usr/share/nginx/html
```

- Push the code to github and run the Dockerfile inside the server.

- Now

```bash
docker build -t web:v1 .
docker run -d -p 80:80 web:v1

```

- Now copy the ip address in browser web page is open.

- ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2efc2c7b-1c87-4d76-9304-a16feb750706/Untitled.png)

- **Docker Networking:**
- Now website is ready but we don't configure the other compents. Now configure the components step by step.
- we will make connection to web to catalogue.

### Catalogue :

- Public will open the web page( frontend) here we need to configure the  **Catalogue** here client will choose the products.
- Copy the content from the reference and put into to our project.
- In this microservice developer developed by **nodejs.**
- Now create a Dockerfile

```bash
FROM node:14
EXPOSE 8080
WORKDIR /opt/server/
COPY package.json /opt/server/
#npm install get the dependencies of node js project
RUN npm install
COPY server.js /opt/server/
ENTRYPOINT ["node","server.js"]
```

- Now server.js file catalogue requires MongoDB.

- For that purpose we have MongoDB.
- 

### **MongoDB** :

- Now copy the mongodb from the reference directory. Then put it into our project.
- Now catalogue needs mongodb.
- Now clearly says that web is dependent on catalogue then catalogue is dependent on MongoDB.
- MongoDB is a database.
- Whenever you goto any e-commerce application lot of products will be their. Those products are generally in database. User information are also stored.
- 
- 
- Now Dockerfile
- 

```bash
FROM mongo:5
COPY *.js /docker-entrypoint-initdb.d/

```

* Initdb.d will load the. Js files.

- Now push the code to github and pull the code to docker server.

Now

```bash
docker build -t mongodb:v1 .
docker run -d mongodb:v1

```

- Now task is mongodb and catalogue should be run and then we will connect mongodb to catalogue. Then those should be connected then web should be connected to catalogue.

1. MongoDB should be running
2. Catalogoue should be running
3. Connect mongodb and catalogue
4. Connect web to catalogue.
5. Containers should have a proper name to connect with each other. Otherwise we will get a random name. It should not connect..
6. By default you are not able to connect name, you can connect to ip address, but their is a problem everytime you create container ip address may change.
7. Thats why we have DNS that is problem in docker networking.
- Now catalogue and mongodb is running how can i connect both?
- J
- Data is present in mongodb then catalogue will load the data.
- Now see the logs inside the catalogue
- 

```bash
docker logs <container id>
```

- In this shown mongo network error. It will not able to connect the mongodb why because now can solve the networking problem between the containers..

- In catalogue server. js it  is refering mongodb name and port number 27017 refers the Catalogue.

- Here only problem is name trying to established a connection name is mongodb. But what is our container name is random name.

- While creating a container proper name is important for the containers connect with each other.

- Now remove all the containers and give proper name

- Now check

```bash
docker logs <container id>
```

```bash
docker build -t catalogue:v1 .
docker run -d Catalogue:v1
```

```bash
docker run -d --name mongodb mongodb:v1
docker run -d --name catalogue Catalogue:v1
```

- Still facing the same issue error.

- Now proper names also not connected

- Now troubleshoot go inside the catalogue container
- 

```bash
docker exec -it catalogue bash
ping mongodb
#name or service not known
ping <ip adreess>
```

- It is not able able to identify

**Docker networking**

- Let us take a example as a home network modem. All the devices are conneted to modem

```bash
docker inspect mongodb | grep -i ip
```

```bash
ipconfig
```

- 

- ![image-1681287556723.jpg6312390167941873069.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b652caa2-2423-4f7a-a003-17bc2567583d/image-1681287556723.jpg6312390167941873069.jpg)

* Docker have some networks.

1. Bridge network ——- by default 
2. Host network
3. Overlay network
4. Macvlan network

- Now to goto catalogue search its shown the network

```bash
docker network ls
```

- By default all the containers shoul

- But their is one problem in default bridge network can't resolve on names.

- Docker recommends to create our own network.

- ![image-1681288142628.jpg8261283134727246031.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66903f11-937b-4df2-9109-e662652284e8/image-1681288142628.jpg8261283134727246031.jpg)

- Lets remove all remove containers and create our own bridge network

```bash
docker network create roboshop
```

- You can isolated or connected the other components to this network.

- Adavantage is containers are isolated from another project.

- We can communicate using the names between the containers.

- Qs : what is bridge network in docker ?

- Ans: Bridge network is default network in docker. We can create bridge network to isolated the containers from the diffrerent projects. And also we can ping or communication between the containers on their names which is not possible in default network..

- Bridge network is exactly same as our home host network

- Ip a

```bash
ip a
docker run -d  --name mongodb mongodb:v1
docker run -d --name catalogue --network roboshop catalogue:v1
```

- Now check

```bash
docker inspect mongodb
docker network ls

```

- But we will connect to our network

```bash
docker network conncet roboshop mongodb
```

- ![image-1681290153632.jpg1522935980870207471.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f4b6a7f9-f5af-46c0-87dd-f1ec917b56e2/image-1681290153632.jpg1522935980870207471.jpg)

- Now catalogue and mongodb are connected eachother.

- Now we will connect web to catalogue. we will put the Catalogue details in **default**.**conf** file.

- Whenever you hit nginx on /api/catalogue —→catalogue service
- Now edit nginx conf file as **default**.**conf.**
- Dockerfile
- 

```bash
FROM nginx
RUN rm -rf /usr/share/nginx/html/index.html
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf
COPY default.conf /etc/nginx/nginx.conf
ADD static /usr/share/nginx/html/
ENV CATALOGUE_HOST="catalogue"
```

- Now push the code and run

```bash
docker build -t web:v1 .
docker run -d -p 80:80 --name web --network roboshop web:v1
```

- Now successfully configure the Catalogue microservice.

- Next USER module.

- ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e839b3a8-be80-4600-bd12-adbac29b35e2/Untitled.png)

### USER

- Next component is USER.
- USER component is developed by node js.
- User needs mongodb now user connected to mongodb then user connect to web.
- Dockerfile
- 

```bash
FROM node:14
EXPOSE 8080
WORKDIR /opt/server
COPY package.json /opt/server/
RUN npm install
COPY server.js /opt/server/
CMD ["node","server.js"]
```

- Then push the code to github and clone to docker server.

```bash
docker build -t user:v1 .
docker run -d --name user --network roboshop user:v1
```

- Now user is running.

- How we will connect web to user again open web configuration file **default.conf.**
- 

```bash
docker build -t web:v1 .
docker run -d --name web -p 80:80 --network roboshop web:v1
```

- ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1a54529-ac04-4fe5-883d-cdc2b426fc1c/Untitled.png)

