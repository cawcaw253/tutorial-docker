## Dockerfile

### Consturct of Dockerfile

도커 파일의 구조

```
Instruction Argument
```

### Explain example Dockerfile

```
FROM Ubuntu // Start from a base OS or another image

RUN apt-get update && apt-get -y install python

RUN pip install flask flask-mysql // Install all dependencies

COPY. /opt/source-code // Copy source code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run // Specify Entrypoint
```

### Layered Architecture

도커는 이미지 빌듯이 레이어 구조로 빌드를 합니다.
하나의 커맨드를 실행할 때마다 이전 레이어와의 변화만을 저장하며 그 크기 또한 저장합니다.
위의 Dockerfile을 예로 들면,
`FROM Ubuntu` 에서 레이어가 이미지의 크기인 120mb의 공간을 지닌다면
`RUN apt-get update && apt-get -y install python` 에서는 레이어가 수정된 apt packages의 크기만 지니게 됩니다.
이러한 레이어의 상세는 `docker history` 커맨드로 확인할 수 있습니다.

#### failure

이러한 레이어 구조는 이미지 빌드가 실패했을 때 다시 처음부터 빌드를 하는 것이 아닌,
에러가 발생한 단계의 이전 레이어는 캐시를 통해 가져옴으로써 같은 작업을 여러 번 하지 않고 빠르게 빌드할 수 있게 해 줍니다.

### ENV Variables in Docker

```
docker run -e ENV_VAR=hello
```

`-e KEY=VALUE` 로 환경변수를 설정할 수 있습니다.

### COMMAND vs ENTRYPOINT

#### Command

```
FROM ubuntu

CMD sleep 5 // CMD ["sleep", "5"]
```

만약 여기서 sleep시간을 10으로 바꾸고 싶다면?

```
docker run ubuntu-sleeper sleep 10
```

커맨드 전체를 overwrite 해서 기존 커맨드를 바꾼다

#### Entrypoint

```
FROM ubuntu

ENTRYPOINT ["sleep"]
```

만약 여기서 sleep시간을 10으로 바꾸고 싶다면?

```
docker run ubuntu-sleeper 10
```

변수 10은 Entrypoint 뒤에 append 되어 사용된다.

#### Difference and topic

위의 예시에서 ENTRYPOINT를 사용하고

```
docker run ubuntu-sleeper
```

로 컨테이너를 실행하면 sleep커맨드에 변수가 지정되지 않아 에러가 발생한다.

여기서 ENTRYPOINT를 사용하면서 Default값을 주는 방법은 어떤 것이 있을까?

```
FROM ubuntu

ENTRYPOINT ["sleep"]

CMD ["5"]
```

해결책으로는 ENTRYPOINT와 COMMAND를 같이 사용하는 방법이 있다.
위의 Docker파일을 사용하면

```
docker run ubuntu-sleeper
```

변수를 사용하지 않으면 `sleep 5` 를 실행하고,

```
docker run ubuntu-sleeper 10
```

변수를 사용 시 CMD의 5를 overwrite 하여 `sleep 10` 이 실행되게 된다.
