* Draft: 2020-07-01 (Wed)

# 쿠버네티스 클러스터 설치하기

쿠버네티스 클러스터 (Kuternetes Cluster)를 두 가지 환경에 만들 수 있습니다.

* 학습 환경
* 운영 환경

여기에선 운영 환경에 쿠버네티스 클러스터를 설치하는 경우를 다룹니다. [쿠버네티스 공식 문서](https://kubernetes.io/ko/docs/home/)의 [시작하기](https://kubernetes.io/ko/docs/setup/) > [운영 환경](https://kubernetes.io/ko/docs/setup/production-environment/)에 해당합니다.

## 운영 환경을 위한 쿠버네티스 클러스터 설치하기

이제부터 모든 명령어는 `root` 권한으로 실행해야 합니다. `root` 계정으로 로그인 하거나 명령어 앞에 `sudo`를 붙이면 됩니다.

### `root` 계정으로 로그인 하기

`sudo -i` 혹은 `sudo -s` 명령어로 `root` 계정으로 로그인할 수 있습니다.

```bash
$ sudo -i
[sudo] password for k8smaster: 
# 
```

```bash
# exit
logout
$
```

프롬프트가 $에서 #으로 바뀌었음에 주의하세요. root 계정의 프롬프트는 #입니다. 현재 $에서는 k8smaster라는 계정을 쓰고 있습니다.

아래에선 이 과정을 조금 더 자세히 설명합니다. `whoami` 명령어는 현재 누구의 계정인지를 리턴해주는 리눅스 명령어 입니다.

```bash
$ whoami
k8smaster
$ sudo -i
[sudo] password for k8smaster: 
#
# whoami
root
# exit
logout
$
$ whoami
k8smaster
$
```

$ 프롬프트에서는 사용자 계정이 k8smaster 였고, `sudo -i` 명령어와 패스워드를 입력해서 로그인했더니, 프롬프트가 #로 바뀌었습니다. `whoami` 명령어로 계정이 누구인지 확인해보니  root였고, `exit` 명령어로 로그아웃했더니 프롬르트가 다시 $로 돌아왔습니다. 계정이 누구인지 재확인해보니 역시나 k8smaster였습니다.

### root 권한으로 명령어를 실행하는 예: `apt update`

`apt update` 명령어를 실행하라고 하면, 아래 두 가지 중 한가지 방식으로 명령어를 실행해야 합니다. 여러 개의 명령어를 입력해야 하므로 가능하다면 root 계정으로 로그인하는게 더 편리합니다.

1. #### root 로 로그인 해서 명령어를 실행

```bash
# apt update
```

2. #### 앞에 `sudo`를 붙이고 명령어를 실행

```bash
$ sudo apt update
```

### 컨테이너 런타임 (Container Runtime) 설치하기

쿠버네티스는 컨테이너 오케스트레이션 툴 (Container Orchestration Tool)이므로, 컨테이너를 다루기 위해 필요한 컨테이너 런타임 (프로그램)의 설치가 선행되어야 합니다. 현재 사용 가능한 컨테이너 런타임은

* [Docker](https://www.docker.com/)
* [CRI-O](https://cri-o.io/) (Container Runtime Interface-Open Container Initiative)
* [rkt](https://coreos.com/rkt/)
* [containerd](https://containerd.io/)

가 있습니다. 

쿠버네티스 공식 문서 ([컨테이너 런타임](https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/))에서는 Docker와 CRI-O 의 설치 방법을 설명합니다. 쿠버네티스는 개발 초기에는 런타임 프로그램으로 Docker를 사용했고, CRI-O는 Docker의 단점을 극복하여 인기가 상승하고 있는 컨테이너 런타임입니다. 

#### Docker 설치하기

여기서는 Docker의 설치만 다룹니다. 설치 과정은 일반적인 Docker 설치 과정과 동일합니다. 

여기까지는 앞에 sudo 를 붙이는 경우도 설명을 합니다만, 앞으로는 root계정으로 명령어를 실행할 것을 권장합니다. 앞으로는 root계정으로 로그인한 것을 가정합니다.

1. ##### root 계정으로 명령어를 실행할 경우

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

##### 2. 앞에 sudo 를 붙이고 명령어를 실행할 경우

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

## 배포 툴을 이용해서 쿠버네티스 설치하기

쿠버네티스 아래의 배포 툴 (Deployment Tool) 중 하나를 선택해서 설치합니다.

* kubeadm
* kops [Kops로 쿠버네티스 설치하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kops/)
* kubespray

이 문서에서는 kubeadm을 이용해서 로컬 머신에 쿠버네티스를 설치하는 과정을 설명합니다. kops와 kubespray는 퍼블릭 클라우드에 쿠버네티스 설치를 도와주는 툴이므로 쓰지 않았습니다.

### 한국어 번역된 쿠버네티스 설치 관련 공식 문서

참고로 쿠버네티스 공식 문서의 [Installing Kubernetes with deployment tools](https://kubernetes.io/ko/docs/setup/production-environment/tools/) 메뉴의 하위 문서를 정리하면 아래 표와 같습니다. 열에는 배포 툴 (kubeadm, kops, kubespray)이 있고, 행에는 영어 문서 제목 (English), 한국어 문서 제목 (Korean), 설치 환경 타입 (Host Type)이 있습니다.

|           | kubeadm                                                      | kops                                                         | kubespray                                                    |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| English   | [Bootstrapping clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/) (9) | [Installing Kubernetes with kops](https://kubernetes.io/docs/setup/production-environment/tools/kops/) | [Installing Kubernetes with Kubespray](https://kubernetes.io/docs/setup/production-environment/tools/kubespray/) |
| Korean    | [kubeadm으로 클러스터 구성하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/) (2) | [Kops로 쿠버네티스 설치하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kops/) |                                                              |
| Host Type | Any(?)                                                       | AWS                                                          | GCE, Azure, OpenStack, AWS, vSphere, Packet (bare metal), Oracle Cloud Infrastructure (Experimental) or Baremetal |

복수의 하위 문서가 있을 경우 개수를 괄호 () 안에 표시했습니다. 2020년 7월 현재 kubeadm의 9개의 영어 문서 중 2개만 한국어로 번역되어 있습니다.

### kubeadm 을 이용한 쿠버네티스 설치

이 부분은 쿠버네티스 공식 문서의 [kubeadm으로 클러스터 구성하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/) 혹은 [Bootstrapping clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/)에 해당합니다. 

* kubeadm 설치하기 / [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

* 클러스터 설정하기
  * kubeadm로 단일 컨트롤 플레인 클러스터 설정하기 / [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
  * [kubeadm로 컨트롤 플레인 사용자 정의하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/control-plane-flags/) / [Customizing control plane configuration with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/control-plane-flags/)
  * kubeadm로 클러스터의 각 kubelet 설정하기 / [Configuring each kubelet in your cluster using kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/kubelet-integration/)

#### kubeadm 설치하기 / [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

##### OS 설치

- Ubuntu 16.04+
- Debian 9+
- CentOS 7
- Red Hat Enterprise Linux (RHEL) 7
- Fedora 25+
- HypriotOS v1.0.1+
- Container Linux (tested with 1800.6.0)

##### 최소 요건

* 각 컴퓨터 혹은 노드의
  * **swap의 기능이 꺼져있다.**
  * CPU가 2개 이상 이다.
  * RAM이 2 GB 이상 이다.
  * hostname, MAC주소, product_uuid가 고유하다. ([here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#verify-mac-address) 참조)
  * 특정 포트가 개방되야 한다. ([here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports) 참조)
* 클러스터의 컴퓨터 혹은 노드가 모두 네트워크로 연결되야 한다.
  * public network 혹은 private network 상관 없음.

**중요: 각 컴퓨터에 설치될 kubelet이 정상 동작하려면 swap의 기능이 꺼져있어야만 합니다.**

##### Step 1. 각 노드의 hostname, MAC주소, product_uuid가 고유한지 확인.



##### [턴키 클라우드 솔루션](https://kubernetes.io/ko/docs/setup/production-environment/turnkey/)
