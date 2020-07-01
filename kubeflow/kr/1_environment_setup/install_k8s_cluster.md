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

여기서는 Docker의 설치만 다룹니다. 설치 과정은 일반적인 Docker 설치 과정과 동일합니다. 쿠버네티스를 설치하고자 하는 모든 컴퓨터 (마스터와 모든 워커 노드)에 먼저 설치해야 합니다.

#### Step 1. Docker 설치하기

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

#### Step 2. Docker 설치 여부 확인하기

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

## 배포 툴을 이용해서 쿠버네티스 설치하기

쿠버네티스 아래의 배포 툴 (Deployment Tool) 중 하나를 선택해서 설치합니다.

* kubeadm
* kops
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

아래는  [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)에서 설명하는 내용입니다.

#### kubeadm 설치 전 사전 확인 작업

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
* 클러스터의 컴퓨터 혹은 노드가 모두 네트워크로 연결될 수 있어야 한다.
  * public network 혹은 private network 상관 없음.

**중요: 각 컴퓨터에 설치될 kubelet이 정상 동작하려면 swap의 기능이 꺼져있어야만 합니다**

##### Step 1. 각 노드의 hostname, MAC주소, product_uuid가 고유한지 확인

마스터로 사용할 컴퓨터

```bash
$ hostname
GPU-Desktop
$ ip link | grep "link"
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    link/ether 14:b3:1f:22:ef:e3 brd ff:ff:ff:ff:ff:ff
    link/ether 9c:b6:d0:ea:33:89 brd ff:ff:ff:ff:ff:ff
    link/ether 02:42:fb:71:1f:45 brd ff:ff:ff:ff:ff:ff
$ sudo cat /sys/class/dmi/id/product_uuid
[sudo] password for k8smaster: 
4C4C4544-0053-3910-8030-C3C04F314C32
$
```

워커 노드로 사용할 컴퓨터

```bash
$ hostname
k8snode-01-gpu-desktop
$ ip link | grep "link"
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    link/ether d8:9e:f3:7b:49:2e brd ff:ff:ff:ff:ff:ff
    link/ether 9c:b6:d0:f5:7e:21 brd ff:ff:ff:ff:ff:ff
$ sudo cat /sys/class/dmi/id/product_uuid
[sudo] password for k8snode: 
4C4C4544-004B-3110-8059-C4C04F504D32
$
```

##### Step 2. 네트워크 어댑터 (Network Adapter) 확인

쿠버네티스 클러스터 주소가 적합한 네트워크 어댑터를 지나갈 수 있도록 IP루트 (IP route)를 추가하기를 추천합니다. 

만약 컴퓨터에 꽂힌 네크워크 카드가 한 개 이상일 경우, 쿠버네티스 구성요소들 (Kubernetes Components)이 디폴트 경로 (default route)로 데이터를 주고 받을 수 없을 수 있습니다.

TODO: 공식 문서의 설명이 부족하므로 필요 시 내용 추가.

##### Step 2.1. Linux노드의 iptables이 bridged traffic을 볼 수 있도록 설정되었는지 확인

##### Step 2.1.1. `br_netfilter` 모듈이 로딩되었는지 확인

```bash
$ lsmod | grep br_netfilter
br_netfilter           24576  0
bridge                155648  1 br_netfilter
$
```

로딩이 안 되었다면, 아래 명령어로 로딩합니다.

```bash
$ sudo modprobe br_netfilter 
```

더 상세한 내용은 [Network Plugin Requirements](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/#network-plugin-requirements)를 참고하세요

##### Step 2.1.2. `net.bridge.bridge-nf-call-iptables`이 1로 설정되었는지 확인

아래 명령어를 실행하기 전에 `br_netfilter` 모듈이 로딩되어 있어야 합니다.

```bash
$ cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
$ sudo sysctl --system
```

위의 명령어는 `/etc/sysctl.d/k8s.conf` 을 생성합니다. 파일 내용은 아래와 같습니다.

```bash
$ cat /etc/sysctl.d/k8s.conf 
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
$
```

`sysctl`명령어을 실행하면  `/etc/sysctl.d/k8s.conf` 의 설정파일이 적용된 것을 확인할 수 있습니다.

```bash
$ sudo sysctl --system
  ...
* Applying /etc/sysctl.d/k8s.conf ...
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
* Applying /etc/sysctl.conf ...
$
```

#####  Step 3. 필요한 필수 포트의 개방 여부를 확인

* 마스터 노드는 6443, 2379-2380, 10250-10252 포트가 필요
* 워커 노드는 10250, 30000-23767 포트가 필요



마스터 노트 (Master Node or Control-Plane Node)

| Protocol | Direction | Port Range | Purpose                 | Used By              |
| -------- | --------- | ---------- | ----------------------- | -------------------- |
| TCP      | Inbound   | 6443*      | Kubernetes API server   | All                  |
| TCP      | Inbound   | 2379-2380  | etcd server client API  | kube-apiserver, etcd |
| TCP      | Inbound   | 10250      | Kubelet API             | Self, Control plane  |
| TCP      | Inbound   | 10251      | kube-scheduler          | Self                 |
| TCP      | Inbound   | 10252      | kube-controller-manager | Self                 |

*가 붙은 포트 (6443)는 덮어쓸 수 있으므로, 이 포트를 쓸 수 있는지 확인해야 합니다.

TODO: 확인하는 명령어가 공식 문서에 없으므로 추가해야 함

워커 노드 (Worker Node)

| Protocol | Direction | Port Range  | Purpose            | Used By             |
| -------- | --------- | ----------- | ------------------ | ------------------- |
| TCP      | Inbound   | 10250       | Kubelet API        | Self, Control plane |
| TCP      | Inbound   | 30000-32767 | NodePort Services† | All                 |

#### kubeadm 설치하기

이 부분은 쿠버네티스 공식 문서의 [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) > [Installing runtime](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-runtime)에 해당합니다.



##### [턴키 클라우드 솔루션](https://kubernetes.io/ko/docs/setup/production-environment/turnkey/)