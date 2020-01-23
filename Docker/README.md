# Docker

This directory for the dockerfile that includes grSim and vision-client softwares
with the needed packages.


### Build

```docker build -t robocup_docker_img .```


### Run

```docker run -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm --name RoboCupSSL robocup_docker_img```

Then enter from the webpage ```127.0.0.1:6080```
or from any VNC server software: ```127.0.0.1:5900```

### Continue working

If you closed the docker container, you can run it again and working on it by:

```docker start -ai RoboCupSSL```
