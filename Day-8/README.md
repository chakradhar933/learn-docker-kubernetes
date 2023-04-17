

### Payment:

- Copy the payment component from the reference dirctory.
- Dockerfile
- 

```bash
FROM python:3.9
EXPOSE 8080
USER root
#ENV INSTANA_SERVICE_NAME=payment
WORKDIR /app
COPY requriements.txt/app/
RUN pip install -r requirements.txt
COPY *.py/app/
COPY payment.ini/app/
#CMD ["python","payment.py"]
CMD ["uwsgi","--ini","payment.ini"]
```

Now docker-compose

```yaml
rabbitmq:
  image:rabbitmq
  container_name: rabbitmq
payment:
  image: payment:v1
  container_name: payment
  depends_on:
  - rabbitmq
ratings:
  image: ratings:v1
  container_name: ratings
  depends_on:
  - mysql

```

## Ratings:

- Also same

Now

1. Container are all ready now push to dockerhub.
2. Main theme of docker is build once run any where.
3. Now we run the simple bash script to push the all the containers to dockerhun at a time
4. Now login to docker

```bash
for i in web mongodb catalogue user cart mysql shipping payment ratings ;do cd $i ; docker build -t chakradhar933/$i:v1 . ; docker push chakradhar933/$i:v1 ; cd .. ; done
```

- Now all the images are ready then push to dockerhub.
- You can do it manually. By using the commands

```bash
docker login
docker build -t chakradhar933/<image name>:version .
docker push chakradhar933/<image-name>:version
```

- Now docker images are ready at dockerhub. Now you can run the images at testing environment or any other you no need to build the images again .
- Main feature of docker is build once and run anywhere.
- Once you build the image you no need to build the image again and again just you run the image next application will be upper running.
- 
- Now you will create new instance
- Install docker and docker-compose then create one docker-compose file
- 

```yaml

```

Now run the run the command

```yaml
docker-compose up -d
```

- Now application is ready and upper running on test instance also.

### Multi stage build :

- Best practices in docker:
1. Keeping the images small. But how can you keep images small?
2. Ans: reduce image and you need ti take care of port. For example this application will run at 2 gb memory to reduce to 1 gb application shoul
3. Application memory should be less and performance should be fast.
4. Next best practice is using non root user.
5. We  need to create the user and give the permissions to that user
6. Now take example for cart

```bash
FROM node:14
EXPOSE 8080
WORKDIR /opt/server/
RUN addgroup cart && adduser cart --system cart && usermod -aG cart cart
RUN chown -R cart:cart /opt/server
USER cart
COPY package.json /opt/server/
RUN ls -lrt
RUN npm install
COPY server.js/opt/server/
CMD ["node", "server. js"]
```

- Ques : Tell me about best pracites while implemented or created docker images
- ans:
1. Use light weight base images like almalinux,busybox etc..,
2. use multi-stage builds for removing the unneccessary installations.
3. Use non-root users
4. Use volumes for statefull applications.
5. Use env variables instead of hard coding.
6. Use dedicated custom networks.
7. Dont kept screts in images.