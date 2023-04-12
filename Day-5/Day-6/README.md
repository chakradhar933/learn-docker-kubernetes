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