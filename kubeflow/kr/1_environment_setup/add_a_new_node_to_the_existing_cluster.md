* Draft: 2020-07-07 (Tue)

# 클러스터에 신규 노드 조인 (Join)하기

기존에 생성된 클러스터에 노드를 새로 조인 (Join) 해봅니다.



컨테이너 런타임 (Container Runtime) 설치하기


## 1. Docker 설치 여부 확인하기

$ hostname
k8snode-01-gpu-desktop
$ docker --version
Docker version 19.03.11, build 42e35e61f3
$

$ sudo docker run hello-world


`/var/run` 디렉토리에서 Docker 혹은 containerd와 관련된 파일을 보면 

```bash
$ cd /var/run
$ ls | egrep "docker|containerd"
containerd
docker
docker.pid
docker.sock
$
```

워커 노드 역시 Docker뿐만 아니라 containerd도 같이 있음을 알 수 있습니다.

## 2. Docker 설치하기

여기까지는 앞에 sudo 를 붙이는 경우도 설명을 합니다만, 앞으로는 root계정으로 명령어를 실행할 것을 권장합니다. 앞으로는 root계정으로 로그인한 것을 가정합니다.

### `root` 계정으로 로그인 하기

`sudo -i` 혹은 `sudo -s` 명령어로 `root` 계정으로 로그인할 수 있습니다.

$ sudo -i
[sudo] password for k8smaster: 
$

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

부팅 후 Docker 서비스를 시작하려면
# systemctl enable docker


## kubeadm, kubelet, kubectl 설치하기

모든 컴퓨터에 kubeadm, kubelet, kubectl를 설치합니다. 

```bash
$ sudo apt-get update && sudo apt-get install -y apt-transport-https curl
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
$ sudo apt-get update
$ sudo apt-get install -y kubelet kubeadm kubectl
$ sudo apt-mark hold kubelet kubeadm kubectl
```

The kubelet is now restarting every few seconds, as it waits in a crashloop for kubeadm to tell it what to do.

워커 노드

$ sudo apt-get update && sudo apt-get install -y apt-transport-https curl
  ...
curl is already the newest version (7.58.0-2ubuntu3.9).
apt-transport-https is already the newest version (1.6.12ubuntu0.1).
0 upgraded, 0 newly installed, 0 to remove and 11 not upgraded.
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
OK
$ cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
> deb https://apt.kubernetes.io/ kubernetes-xenial main
> EOF
> deb https://apt.kubernetes.io/ kubernetes-xenial main
> $ sudo apt-get update
> ...
> Reading package lists... Done
> $ sudo apt-get install -y kubelet kubeadm kubectl
> ...
> Setting up kubectl (1.18.5-00) ...
> Setting up ethtool (1:4.15-0ubuntu1) ...
> Setting up kubelet (1.18.5-00) ...
> Created symlink /etc/systemd/system/multi-user.target.wants/kubelet.service → /lib/systemd/system/kubelet.service.
> Setting up kubeadm (1.18.5-00) ...
> Processing triggers for systemd (237-3ubuntu10.41) ...
> Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
> Processing triggers for ureadahead (0.100.0-21) ...
> $ sudo apt-mark hold kubelet kubeadm kubectl
> kubelet set on hold.
> kubeadm set on hold.
> kubectl set on hold.
> $


## 노드 설정:  `kubeadm join`명령어로 클러스터에 조인 (join)하기

앞서 생성된 클러스터에 노드를 조인 (join) 하기 위해,   `kubeadm join`명령어를 실행합니다. 상세한 내용은 쿠버네티스 공식 문서의 [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) > [join nodes to your cluster](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#join-nodes)를 참고하세요.

#### Step 1.  노드에서 `kubeadm join`명령어 실행

```bash
$ kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

에 해당하는 명령어를 실행합니다. 구체적인 파라미터 값은 마스터에서 `kubeadm init` 명령어 실행 시 출력됩니다. 예를 들면,

```bash
$ sudo kubeadm join 192.168.0.109:6443 --token zqw1lb.tuhllf8m7zntibcq \
    --discovery-token-ca-cert-hash sha256:e3f15962b0535847add930d0e16fe92dc3e7ed139f29e0093e0b0766ca615671
```

출력 메세지는

[sudo] password for k8snode: 
W0703 19:13:46.603764   24337 join.go:346] [preflight] WARNING: JoinControlPane.controlPlane settings will be ignored when control-plane flag is not set.
[preflight] Running pre-flight checks
[preflight] Reading configuration from the cluster...
[preflight] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[kubelet-start] Downloading configuration for the kubelet from the "kubelet-config-1.18" ConfigMap in the kube-system namespace
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Starting the kubelet
[kubelet-start] Waiting for the kubelet to perform the TLS Bootstrap...

This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
$

이 노드가 클러스터에 조인 (join) 했고, 확인하려면 컨트롤 플레인 (the control-plane), 즉 마스터에서 `kubectl get nodes`명령어를 실행하라는 메세지가 출력됐습니다. 이렇게 해서 단일 구성 클러스터의 생성을 완료했습니다. 