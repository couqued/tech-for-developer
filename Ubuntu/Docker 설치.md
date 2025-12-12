vi /etc/apt/apt.conf (proxy 확인)
sudo vi /etc/systemd/system/docker.service.d/proxy.conf (도커 proxy 설정)

FTP 연결
 - sudo apt install net-tools
 - sudo apt-get install vsftpd
 - sudo service vsftpd restart
 - sudo vi /etc/vsftpd.conf
   : #write enable=YES 주석제거
 - sudo /etc/init.d/vsftpd restart

파이썬 설치
 - python3 --version
 - pip3 --version
 - sudo apt install python-pip

톰캣 search
 - sudo docker search tomcat

httpd pull
 - sudo docker pull httpd

도커설치
 - sudo apt-get update
 - sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common (도커설치)
 - sudo apt-get install docker-ce docker-ce-cli containerd.io
 
로그인된 사용자 확인
 - aws sts get-caller-identity
	
도커 시작
 - sudo /etc/init.d/docker start
 
aws cli 설치
 - sudo apt install curl unzip
 - (sudo apt install fpzip-utils)

 - curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

 - unzip awscliv2.zip
 - sudo ./aws/install
 - aws --version

---

Docker 설치방법

1. 우분투 시스템 패키지 업데이트
sudo apt-get update

2. 필요한 패키지 설치
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
 
3. Docker의 공식 GPG키를 추가
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 
4. Docker의 공식 apt 저장소를 추가
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

5. 시스템 패키지 업데이트
sudo apt-get update

6. Docker 설치
sudo apt-get install docker-ce docker-ce-cli containerd.io
 
7. Docker가 설치 확인

7-1 도커 실행상태 확인
sudo service docker status
sudo systemctl status docker

7-2 도커 실행
sudo service docker start
sudo docker run hello-world

7-3 도커 재기동
sudo service docker restart
