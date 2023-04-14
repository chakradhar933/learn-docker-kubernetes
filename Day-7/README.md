####3
- Create one new ec2 instance size t2 medium instance launch instance.
- Now install docker in ec2 instance

- Their are lot of service the difficulty is 1st thing

1. First we neeed to build the image. (Developer build the image in realtime)
2. He will push to docker hub.
3. All images should be available in dockerhub
4. Then we can define the dependency and run the containers. For once the all the images are available you no need to run the containers one by one for that purpose we have something called **Docker Compose.**
5. The adavantage of docker compose is instead of running containers one by one you can stop and start the containers, define the dependencys everything in the file.
6. For you know docker commands like
- Docker run, docker ps : these comands are used . Docker run command is download the image and runs the container. Instead of doing we are learn Dockerfile
- Dockerfile
- Similarly instead of running and creating containers are running one by one in a proper way .
- You can define the dependencys in **docker-compose.yaml** file

## Docker-compose.yaml

1. Can start all the containers at a time
2. Can stop all at a time
3. Define networking
4. Define volumes.
- Just install docker-compose of command line

```bash
- sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose version
```

Now write docker-compose file

- Docker-compose.yaml
- Services are nothing but what are all the containers you will run.

```yaml
version: "3.9"
networks:
  roboshop:
    driver: bridge
services:
  web:
    image: web:v1
    container_name: web
    ports:
    - "80:80"
    depends_on:
    - catalogue
    - user

  mongodb:
    image: mongodb:v1
    container_name: mongodb
  catalogue:
    image: catalogue:v1
    container_name: catalogue
    depends_on:
    - mongodb
  redis:
    image: redis
  user:
    image: user:v1
    container_name: user
    depends_on:
    - mongodb
    - redis
  cart:
    image: cart:v1
    container_name: cart
    depends_on:
    - redis
    - catalogue
  mysql:
    image: mysql:v1
    container_name: mysql
  shipping:
    image: shipping:v1
    container_name: shipping
    dependa_on:
    - mysql
```

- Now push the code to github and pull the code.
- 1st we will build a docker images
```yaml
docker build -t web:v1 .
docker build -t catalogue:v1 .
docker build -t mongodb:v1.
```
## Yaml syntax :

- Yaml is used to write ansible scripts, cloudformation scripts, Kubernetes etc.,
- YAML  ——> Yet Another Markup Language.
- HTML ——> Hyper text markup language.
## Data transfer object :

- Xml ——> Extensible markup language.
- Json ——> Java script object notation.
- YAML.
- What is the use of those languages is for example you will login facebook then login with personal details. Data will transfer the facebook server.
- **Xml** :
- Xml format is nothing but
- <Username>chakri</username>
- Multiple address is nothing but list of address.
- Map is nothing but multiple key value pairs here key —→ permenaddress ——> Map
```xml
<Username>chakri</username>
<password>chakri123</password>
<Address>
   <permaddress>
      <doorno></doorno>
      <street></street>
   </premaddress>
   <Currentaddress>
   </Cureentaddress>
</Address>
```
- **YAML :**
- YAML  works on indentation.
- How can you write yaml?
- Here list starts with -
- Perm and curr is mentions as diffrent objects

```yaml
username:"chakradhar"
password:"chakri123"
address:
- type:"perm"
  doorno:123
  street:"streer123"
  city:"rjy"
-type:"current"
 doorno:123
 street:"stty"
 city:"rjy"

```
### Shipping:
- Copy the shipping compoents by the reference project.
- Shipping component is developed by java. Shipping data will be at mysql database.
- Java project is little tricky.
- For java projects have dependences on pom.xml
- Mvn install or mvn package it install the dependendeces and output as .jar files.
