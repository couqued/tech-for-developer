# Kubernetes Pod

#### 1. Pod 생성

``` bash
$ kubectl create deploy tc --image=tomcat:9.0 --replicas=5
```
<br />

#### 2. 생성된 Pod 기동
``` bash
$ kubectl expose deploy tc --type=LoadBalancer --port=80 --target-port=8080
```
<br />

#### 3. 기동된 Pod 확인
``` bash
$ kubectl get pod,svc
```

#### 4. yaml 파일 생성하기
``` bash
$ kubectl create -f go-http-pod.yaml
```

#### 5. pod 정보 보기
``` bash
$ kubectl get pod http-go -o wide
```

#### 6. yaml 파일 보기
``` bash
$ kubectl get pod http-go -o wide
```

#### 7. pod 정보 상세 보기
``` bash
$ kubectl describe pod http-go
```
