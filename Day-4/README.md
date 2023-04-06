### ENTRYPOINT :
- Most popular question in docker is what is tha diffrence between CMD and ENTRYPOINT.
- Next instruction is ENTRYPOINT.
- ENTRYPOINT is also used to run the container just like CMD. But there are few diffrences.
- Main diffrence is we can't override ENTRYPOINT, but we can override CMD
- We can't overide ENTRYPOINT, if you try to do so it will go and append to ENTRYPOINT command.
- If you use CMD and ENTRYPOINT and don't give any command from terminal, CMD acts as a argument provider to ENTRYPOINT.
- CMD will supply default arguments to ENTRYPOINT.
- You can always overide CMD argument from runtime.
- We can stop misusing your image with other commands.
- Now best results we can give is

```bash
FROM almalinux
CMD ["google.com"]
ENTRYPOINT ["ping","-c4"]
```

```bash
FROM almalinux
CMD ["ping","-c5","google.com"]
```

- Now see what command is run backside is

```bash
docker ps -a --no-trunc
```
### USER
- It is used to run the commands as a particular user.
```bash
FROM almalinux
RUN adduser nginx
USER nginx
RUN touch /tmp/hello.txt
```

### WORKDIR
- WORKDIR is used to set the path to the docker image while creating.
```bash
FROM almalinux
#RUN cd /tmp/
WORKDIR /tmp
RUN touch hello.txt
```
## ARG

- ARG is used to supply some variables at the image creation.
- What is the diffrence between ARG and ENV?
- Ans : ARG is used only for the image creation. ENV is used both image and container Creation.
- What should be 1st instruction in dockerfile?
- Ans: you can say FROM but an exception you we use ARG.
- ARG is the only instruction before FROM. ARG declared before can't be accesed after from instruction

```bash
ARG VERSION
FROM almalinux:${VERSION-8}
ARG GREETING="HELLO"
ENV GREETS=${GREETING}
RUN echo "$GREETING"
RUN echo "$VERSION"
```

### Using ENV and ARG for best results.

1. Creare one ENV variable and assign the value to ARG to that.
2. Then we can access ARG values through ENV both image and container.
3. 

## ONBUILD

- ONBUILD is used to set some hard guidelines to the image.
- We can control how others can use our image as the base OS.
- 

```bash
FROM almalinux
RUN yum install nginx -y
# when image creater is running this below command is not run
ONBUILD ADD simple.txt/tmp/
```

## STOPSIGNAL

- STOPSIGNAL is used to how to exit the container.
- By dafault docker request for exit and wait for some time.
- If it is not exiting it can force kill.
- Why is this used to when your container received STOPSIGNAL your application can perform
- Ans: you can close db connection and you can do some backup.