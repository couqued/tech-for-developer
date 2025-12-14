### Docker 명령어

- 캐시 제거 후 빌드
``` bash
$ docker build --no-cache -t <image-name> .
```
<br />

- 로컬에서 도커 이미지 실행
``` bash
$ docker run -d -p 5000:5000 --name <실행될 container 명> <Image 명>
```
<br />

- 도커 실행 후 컨터이너 접속하기 (종료 시 컨테이너 삭제 옵션 포함)
``` bash
$ docker run -it --rm <container-name> sh
```
<br />

- dockerfile에서 ssl 우회해서 npm install 하기
``` bash
RUN npm config set strict-ssl false
```
<br />

- 도커 프로세스 확인
``` bash
$ docker ps
$ docker ps -a
```
<br />

- 도커 실행 어플리케이션 로그 확인
``` bash
$ docker logs <container-name>
```
<br />

- 도커 실행 어플리케이션 실시간 로그 확인
``` bash
$ docker logs -f <container-name>
```
<br />

- 도커 컨테이너 삭제
``` bash
$ docker rm <container-name>
```
<br />

- 도커 이미지 삭제
``` bash
$ docker rmi <image-name>
```
<br />

- 도커 컴포즈 빌드
``` bash
$ docker-compose up --build
```
<br />

- 도커 컴포즈 설정 확인
``` bash
$ docker-compose config
```
<br />
