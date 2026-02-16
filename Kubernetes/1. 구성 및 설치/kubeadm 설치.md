# kubeadm 설치

### 대상 환경
- Ubuntu 22.04 / 20.04 LTS
- Control Plane + Worker 노드 구성
- Container Runtime: containerd
- CNI: Cilium
- Kubernetes v1.34 기준


### swap 비활성화
Kubernetes는 Swap이 활성화되어 있으면 kubelet이 정상 동작하지 않습니다.
``` bash
# 현재 시스템에 적용(리부팅하면 재설정 필요)
sudo swapoff -a

# 리부팅 필수
sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab

# 확인
free -h 
```
<br />

### Container Runtime 설치 (containerd)
Kubernetes는 컨테이너 런타임이 필요합니다.
현재 Docker보다 containerd 사용이 권장됩니다.

- Using Docker Repository
``` bash
sudo apt update

sudo apt install -y ca-certificates curl gnupg lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```
<br>

- containerd 설치
``` bash
sudo apt update

sudo apt install -y containerd.io
#sudo systemctl status containerd  # Ctrl + C 눌러서 나간다.
```
<br>

- 쿠버네티스 사용을 위한 containerd를 runtime으로 등록
``` bash
cat <<EOF | sudo tee -a /etc/containerd/config.toml
[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
[plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
SystemdCgroup = true
EOF

sudo sed -i 's/^disabled_plugins \=/\#disabled_plugins \=/g' /etc/containerd/config.toml

sudo systemctl restart containerd
```
<br>

- 소켓이 있는지 확인
``` bash
ls /var/run/containerd/containerd.sock
```
<br>


# kubeadm 설치
(https://v1-34.docs.kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
``` bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

# sudo mkdir -p -m 755 /etc/apt/keyrings

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.34/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# 이 명령어는 /etc/apt/sources.list.d/kubernetes.list 에 있는 기존 구성을 덮어쓴다.
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.34/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
<br>


# 넷필터 브릿지 설정 (커널 모듈 및 네트워크 설정)
브릿지 트래픽과 iptables 연동을 위해 필수 설정입니다.
``` bash
sudo -i

modprobe br_netfilter
echo 1 > /proc/sys/net/ipv4/ip_forward
echo 1 > /proc/sys/net/bridge/bridge-nf-call-iptables

exit
```
<br>


# 마스터 노드 (Control Plane) 초기화
``` bash
sudo kubeadm init
```
<br>

- master node kubectl 사용 설정
``` bash
mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
<br>

- Root 사용자일 경우
``` bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```
<br>

- 확인
(아직 NotReady 상태일 수 있습니다.)
``` bash
kubectl get nodes
```
<br>

# CNI 설치 (Cilium)
Pod 간 통신을 위해 CNI 플러그인 설치가 필요합니다.
(https://kubernetes.io/docs/tasks/administer-cluster/network-policy-provider/cilium-network-policy)

- Cilium CLI 설치
``` bash
curl -LO https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-amd64.tar.gz

sudo tar xzvfC cilium-linux-amd64.tar.gz /usr/local/bin

rm cilium-linux-amd64.tar.gz
```
<br>

- Cilium CLI 설치
``` bash
cilium install
```
<br>

- Cilium CLI 설치 완료 후 (Node Status가 READY 상태로 변경됩니다.)
``` bash
kubectl get nodes
```
<br>

# Worker Node Join
Control Plane에서 출력된 명령을 Worker 노드에서 실행하여 Control plain에 Join 합니다.

- worker node 초대
``` bash
kubeadm join 10.10.10.10:1234 --token <token> \
--discovery-token-ca-cert-hash sha256:<hash>
```
<br>

- 토큰을 잃어버렸을 경우 재출력
``` bash
kubeadm token create --print-join-command
```
<br>

# 노드 상태 확인
``` bash
kubectl get nodes
kubectl get pods -A
```
<br>


