### Docker commands

- docker run `<image>` :
  running docker image, if images not exists pull image and running it
  - -d
    running container and back to prompt
- docker ps :
  list containers
  - -a
    includes stopped containers
- docker stop :
  stop running container
- docker rm `<image>` :
  remove a container
- docker images :
  list all images
- docker rmi `<image>` :
  delete remove images (all version)
- docker pull `<image>` :
  pull only image, not run image
- docker exec `<image>` `<commands>` :
  execute a command inside of running container

### \* 추가설명

만약 `docker run ubuntu` 를 실행한다면, 이미지를 생성하고 바로 종료될 것입니다.
이렇게 되는 이유는 컨테이너는 가상 머신처럼 OS를 host하지 않기 때문입니다.

컨테이너는 웹서버의 인스턴스를 호스팅, 데이터베이스, 분석작업과 같은 특정한 작업이나 프로세스를 실행시키는 역할을 합니다.

한번 작업을 완료하면 컨테이너는 종료되며, 컨테이너는 오직 프로세스가 움직이는 동안에만 동작합니다.
만약 컨테이너 안에서 웹서비스 등이 멈추거나 충돌이 일어나면 컨테이너는 종료되게 됩니다.

이것이 위에서 언급한 바로 종료되는 이유입니다.
우분투는 단지 애플리케이션 베이스가 되는 OS의 이미지로, 애플리케이션 안에 어떠한 프로세스도 존재하지 않기 때문에 `docker run ubuntu` 를 실행해도 바로 종료되는 것입니다.
