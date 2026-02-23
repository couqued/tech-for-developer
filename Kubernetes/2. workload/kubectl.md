- 실제로 생성하지 않고, 클라이언트 측에서 생성 가능 여부만 미리 확인하는 명령어

``` bash
kubectl create deploy nx --image=nginx --dry-run=client
```

<img width="637" height="32" alt="image" src="https://github.com/user-attachments/assets/39049e30-d211-4581-92a3-63525353e2a0" />
<br>

- 실제 생성 없이, 해당 Deployment의 YAML 매니페스트 내용을 출력하는 명령어
``` bash
kubectl create deploy nx --image=nginx --dry-run=client -o yaml
```
<img width="706" height="346" alt="image" src="https://github.com/user-attachments/assets/a16504b7-cc41-4f39-be5d-f121e5879d82" />
<br>

- Kubectl 치트 시트 (자동완성) <br>
(https://kubernetes.io/ko/docs/reference/kubectl/cheatsheet/)

``` bash
source <(kubectl completion bash) # bash-completion 패키지를 먼저 설치한 후, bash의 자동 완성을 현재 셸에 설정한다
echo "source <(kubectl completion bash)" >> ~/.bashrc # 자동 완성을 bash 셸에 영구적으로 추가한다
```

``` bash
alias k=kubectl
complete -o default -F __start_kubectl k
```
