
# Docker 이미지 저장 구조
#### Docker는 컨테이너를 실행하기 위해 이미지를 레이어 구조로 관리합니다.

#### Docker 기본 저장 경로는 Linux 기준 /var/lib/docker 입니다.

#### /var/lib/docker/image
- imagedb : 이미지 메타데이터
- layerdb : 이미지 레이어 정보

#### /var/lib/docker/overlay2
- 실제 데이터가 저장되는 위치

#### 이미지 레이어 동작 구조
- Base OS Layer -> Package Layer -> Application Layer

#### 이미지 실행 흐름
1. docker pull
2. imagedb 에 메타데이터 저장
3. layerdb 에 레이어 정보 등록
4. 실제 파일은 overlay2 에 저장
5. 컨테이너 실행 시 레이어들을 overlay mount

# Docker 명령어

### 특정 경로 용량 조회
``` bash
$ du -sh /var/lib/docker
```

### docker 이미지 정보 조회
``` bash
$ docker inspect tc
```

### container id만 출력
``` bash
#(-q는 container id만 출력)
$ docker ps -a -q

#(이렇게 사용)
$ docker stop `docker ps -a -q`

#(이렇게 사용)
$ docker rm `docker ps -a -q`
```
