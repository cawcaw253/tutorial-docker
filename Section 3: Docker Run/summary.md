## Docker Run

### RUN - TAG

`docker run redis`

using default tag: latest, using image version latest

`docker run redis:4.0`

using image version 4.0

### RUN - STDIN

`docker run -i kodekloud/simple-prompt-docker`

-i means interactive

you can input

`docker run -it kodekloud/simple-prompt-docker`

-t means terminal

you can also show prompt

### RUN - PORT mapping

`docker run kodekloud/simple-webapp`

running on http://0.0.0.0:5000/ -> you cannot access because that port 5000 is for internal docker host

`docker run -p 80:5000 kodekloud/simple-webapp`

now you can access from port number 80

```
docker run -p 80:5000 kodekloud/simple-webapp <-- running on different container
docker run -p 8000:5000 kodekloud/simple-webapp <--
docker run -p 3306:3306 mysql <-- running on different container
docker run -p 8306:3306 mysql <--
```

also youcan run multiple container with different ports

### RUN - Volume mapping

```
docker run mysql

docker stop mysql
docker rm mysql
```

if you stop and remove running mysql container with following commands, you cannot access mysql data, because the data is only keeping inside containers

`docker run -v /opt/datadir:/var/lib/mysql mysql`

you can find data from `/opt/datadir` even container stopped or removed

### Inspect Container

`docker inspect <id or name of container>`

you can watch detail of container

### Container Logs

`docker logs <id or name of container>`

you can watch logs of specific container
