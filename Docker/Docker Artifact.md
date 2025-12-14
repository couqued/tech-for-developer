### Docker 아티팩트 유형
- 도커 아티팩트(Docker Artifact)는 컨테이너 기반 애플리케이션의 빌드, 배포, 운영 과정에서 생성·관리되는 산출물을 의미한다.
- 주요 아티팩트는 이미지(Image) 를 중심으로 하며, 태그·다이제스트·매니페스트·레이어 등으로 구성된다.
<br />

> 1. 단일 아티팩트 (Single Artifact)
 - 하나의 플랫폼(아키텍처)에 대해서만 빌드된 Docker Image
 - ECR에서 보이는 형태 : Image 1개 (Image Index 없음)
<br />

> 2. 멀티 아티팩트 (Multi Artifact)
 - 하나의 태그에 여러 물리 이미지가 연결된 구조
 - 이미지가 여러 개라서 멀티 아티팩트가 아닌 하나의 이미지에 여러 아키텍처용 이미지 인덱스로 구성됨
 - ECR에서 보이는 형태 : Image와 Image Index 존재
 - Image Index (Manifest List)
     ├─ Image (linux/amd64)
     └─ Image (linux/arm64)
<br />

> 3. 멀티 아티팩트로 빌드될 때 단일 아티팩트로 변경하는 방법
 - docker build 전, 아래 설정 추가
``` bash
$ set DOCKER_BUILDKIT=0
$ net stop com.docker.service
$ docker info
$ net start com.docker.service
```
<br />

 - C:\Users\${user}\.docker\daemon.json 파일에 아래 내용 추가
``` bash
 "features": {
	 "buildkit": false
 }
```
