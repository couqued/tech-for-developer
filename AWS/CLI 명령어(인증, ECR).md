> 1. aws configure 지정
``` bash
aws configure --profile <aws 계정>
```
<br />

> 2. AccessKey, SecretKey 정보 입력
``` bash
aws access key id : <AccessKey>
aws secret access key : <SecretKey>
default region name : ap-northeast-2
default output format : json
```
<br />

> 3. AWS PROFILE 지정 및 필요한 경우 PROXY 설정 (OS별 구분)
``` bash
linux/mac
export AWS_PROFILE=<aws 계정>
export HTTP_PROXY=<IP:port>
export HTTPS_PROXY=<IP:port>

window
set AWS_PROFILE=<aws 계정>
set HTTP_PROXY=<IP:port>
set HTTPS_PROXY=<IP:port>

Windows PowerShell
$AWS_PROFILE = '<aws 계정>'
$HTTP_PROXY = '<IP:port>'
$HTTPS_PROXY = '<IP:port>'
```
<br />

> 4. MFA를 이용한 ACCESS KEY 발급  
> (ssl 인증 skip 옵션 : --no-verify-ssl)
``` bash
aws sts get-session-token --serial-number arn:aws:iam::<AWS Account ID>:mfa/<MFA Device 명> --duration-seconds 28800 --token-code ${code}
```
<br />

> 5. 인증에 필요한 KEY, TOKEN 정보 설정 (OS별 구분)
``` bash
linux/mac
export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
export AWS_SESSION_TOKEN=${AWS_SESSION_TOKEN}

window
set AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
set AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
set AWS_SESSION_TOKEN=${AWS_SESSION_TOKEN}
```
<br />

> 6. ecr 로그인
> (ssl 인증 skip 옵션 : --no-verify-ssl)
``` bash
aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com
```
<br />

> 7. AWS ECR(Elastic Container Registry)에 저장된 컨테이너 이미지 목록과 메타데이터를 조회
> (ssl 인증 skip 옵션 : --no-verify-ssl)
``` bash
aws ecr describe-images --repository-name <repository name>
```
예시
``` bash
{
  "imageDetails": [
    {
      "imageDigest": "sha256:abc123...",
      "imageTags": ["latest", "v1.2.3"],
      "imagePushedAt": "2025-09-01T03:21:45+00:00",
      "imageSizeInBytes": 345678901
    }
  ]
}
```
필드	의미  
 - imageDigest	: 이미지의 고유 해시 (불변)  
 - imageTags	: latest, v1.0.0 같은 태그  
 - imagePushedAt :	ECR에 푸시된 시각  
 - imageSizeInBytes : 이미지 전체 크기
<br />

> 8. docker image tag 지정
``` bash
docker tag app-sample:latest <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com/app-sample:v0.0.1
docker tag <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com/app-sample:v1.2 <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com/app-sample:v1.3
```
<br />

> 9. Image를 ECR에 push
``` bash
docker push <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com/app-sample:v1.3
```
<br />

> 10. ECR에 등록되어 있는 이미지를 로컬로 가져오기
``` bash
docker pull <AWS Account ID>.dkr.ecr.ap-northeast-2.amazonaws.com/app-sample:1.3
```
<br />

> 11. ECR 이미지 취약점 스캔(Image Scan) 결과를 조회
> 1) 이미지 태그로 지정
``` bash
aws ecr describe-image-scan-findings --repository-name app-sample --image-id imageTag=v0.1.2
```

> 2) 다이제스트로 이미지 지정
``` bash
aws ecr describe-image-scan-findings --repository-name app-sample --image-id imageDigest=sha256:6j20fhu9202jfjf02fha03afko2
```

