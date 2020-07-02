* Draft: 2020-07-01 (Wed)

# 컨테이너 런타임 (Container Runtime) 설치하기

쿠버네티스는 컨테이너 오케스트레이션 툴 (Container Orchestration Tool)이므로, 컨테이너를 다루기 위해 필요한 컨테이너 런타임 (프로그램)의 설치가 선행되어야 합니다. 현재 사용 가능한 컨테이너 런타임은

* [Docker](https://www.docker.com/)
* [CRI-O](https://cri-o.io/) (Container Runtime Interface-Open Container Initiative)
* [rkt](https://coreos.com/rkt/)
* [containerd](https://containerd.io/)

가 있습니다. 

쿠버네티스 공식 문서 ([컨테이너 런타임](https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/))에서는 Docker와 CRI-O 의 설치 방법을 설명합니다. 쿠버네티스는 개발 초기에는 런타임 프로그램으로 Docker를 사용했고, CRI-O는 Docker의 단점을 극복하여 인기가 상승하고 있는 컨테이너 런타임입니다. 

여기서는 Docker의 설치만 다룹니다. 설치 과정은 일반적인 Docker 설치 과정과 동일합니다. 쿠버네티스를 설치하고자 하는 모든 컴퓨터 (마스터와 모든 워커 노드)에 먼저 설치해야 합니다.

## 1. Docker 설치하기

여기까지는 앞에 sudo 를 붙이는 경우도 설명을 합니다만, 앞으로는 root계정으로 명령어를 실행할 것을 권장합니다. 앞으로는 root계정으로 로그인한 것을 가정합니다.

### 1.1. root 계정으로 명령어를 실행할 경우

```bash
# apt-get update && apt-get install -y apt-transport-https ca-certificates curl software-properties-common gnupg2
# curl -fsSL https://download.docker.com/linux/ubuntu/gpg |  apt-key add -
# add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
# apt-get update &&  apt-get install -y \
  containerd.io=1.2.13-2 \
  docker-ce=5:19.03.11~3-0~ubuntu-$(lsb_release -cs) \
  docker-ce-cli=5:19.03.11~3-0~ubuntu-$(lsb_release -cs)
# cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
# mkdir -p /etc/systemd/system/docker.service.d
# systemctl daemon-reload
# systemctl restart docker
```

부팅 후 Docker 서비스를 시작하려면

```bash
# systemctl enable docker
```

### 1. 2. 앞에 sudo 를 붙이고 명령어를 실행할 경우

```bash
$ sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common gnupg2
$ sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
$ sudo apt-get update && sudo apt-get install -y \
  containerd.io=1.2.13-2 \
  docker-ce=5:19.03.11~3-0~ubuntu-$(lsb_release -cs) \
  docker-ce-cli=5:19.03.11~3-0~ubuntu-$(lsb_release -cs)
$ cat > daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
$ sudo mv daemon.json /etc/docker/
$ sudo mkdir -p /etc/systemd/system/docker.service.d
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

부팅 후 Docker 서비스를 시작하려면

```bash
$ sudo systemctl enable docker
```

##### `cat > daemon.json <<EOF ...`의 sudo용 명령어 변환

일반적으로 명령어 앞에 sudo 만 붙이면 되지만, 그것보다 조금 까다로운 상황이 발생하기도 합니다. 일례로 root계정에서 실행한 아래 명령어 하나는 

```bash
# cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

sudo를 쓰는 경우로 변환할 때, 두 개의 명령어로 나누었습니다.

```bash
$ cat > daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
$ sudo mv daemon.json /etc/docker/
```

## 2. Docker 설치 여부 확인하기

마스터에서 확인하기

```bash
$ hostname
k8smaster-gpu-desktop
$ docker --version
Docker version 19.03.12, build 48a66213fe
$
```

워커 노드에서 확인하기

```bash
$ hostname
k8snode-01-gpu-desktop
$ docker --version
Docker version 19.03.11, build 42e35e61f3
$
```

거의 같은 시간에 설치했지만 워커 노트에 설치한 Docker 의 마이너 버전이 하나 낮네요. 큰 문제는 없으므로 일단 넘어갑니다.

## 다음

* [배포 툴을 이용해서 쿠버네티스 설치하기](install_k8s_with_deployment_tools.md)