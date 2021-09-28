##

### Image

```
docker run nginx

image: nginx
```

도커에서 이미지를 실행, 빌드할 때 이 이미지는 일종의 협약을 따릅니다.

```
image: nginx/nginx    // {User/Account}/{Image/Repository}
```

이 이러한 이미지들은 Registry에서 가져옵니다.

```
image: docker.io/nginx/nginx // {Registry}/{User/Account}/{Image/Repository}
```

기본적으로는 `docker.io`라는 레지스트리에서 이미지를 가져옵니다.
도커에서 제공하는 레지스트리 외에도 다양한 레지스트리가 존재합니다. 예를 들면 구글에서 제공하는 아래와 같은 레지스트리 등과 같이 말입니다.

```
gcr.io/kubernetes-e2e-test-images/dnsutils
```

### Private Registry

private registry를 사용하기 위해서는 로그인이 필요합니다.

```
docker login private-registry.io
```

로그인 후 아래와 같이 레지스트리의 이미지를 사용할 수 있습니다. 만약 로그인을 하지 않았다면 이미지가 없다고 응답될 것입니다.

```
docker run private-registry.io/apps/internal-app
```

### Deploy Private Registry

```
docker run -d -p 5000:5000 --name registry registry:2
```

아래와 같은 커맨드로 이미지를 push/pull 할 수 있습니다.

```
docker image tag my-image localhost:5000/my-image

docker push localhost:5000/my-image

docker pull localhost:5000/my-image

docker pull 192.168.56.100:5000/my-image
```
