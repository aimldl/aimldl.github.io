* Rev.1: 2020-07-03 (Fri)
* Draft: 2020-07-02 (Thu)

# kubeadm init으로  단일 구성 클러스터 생성하기

## 개요

앞서 마스터 노드 초기화의 목표에서 마스터 노드로 사용할 컴퓨터의 대수에 따라

* 단일 구성 클러스터(Single Control-Plane Kubernetes Cluster)
* 고가용성 클러스터  (High Availability Kubernetes Cluster)

중 하나를 선택할 수 있고, 

* [Canal](https://github.com/tigera/canal/tree/master/k8s-install), [Calico](https://docs.projectcalico.org/latest/introduction/), [Cilium](https://github.com/cilium/cilium), [CNI-Genie](https://github.com/Huawei-PaaS/CNI-Genie), [Contiv](http://contiv.github.io), [Contrail](http://www.juniper.net/us/en/products-services/sdn/contrail/contrail-networking/), [Flannel](https://github.com/coreos/flannel/blob/master/Documentation/kubernetes.md), [Knitter](https://github.com/ZTE/Knitter/), [Multus](https://github.com/Intel-Corp/multus-cni), [OVN4NFV-K8S-Plugin](https://github.com/opnfv/ovn4nfv-k8s-plugin), [NSX-T](https://docs.vmware.com/en/VMware-NSX-T/2.0/nsxt_20_ncp_kubernetes.pdf), [Nuage](https://github.com/nuagenetworks/nuage-kubernetes/blob/v5.1.1-1/docs/kubernetes-1-installation.rst), [Romana](http://romana.io), [Weave Net](https://www.weave.works/docs/net/latest/kube-addon/)

중 하나를 Pod Network으로 선택할 수 있다고 설명했습니다.

이 부분에서는 단일 구성 클러스터를 생성하고, Calico Pod Network를 구성하는 명령어에 대해 알아봅니다.

## 전제 조건 (Prerequisites)쿠버네티스 공식 문서의 [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) > 

이 부분은 [kubeadm 설치 전 사전 확인 작업](verify_before_installing_k8s.md) > 4. 스왑 메모리 (Swap Memory) 비활성화에서 이미 설정한 부분이므로 명령어를 요약해봅니다. 중요하므로 클러스터에 쓸 모든 컴퓨터에서 아래의 두 개 명령어를 다시 실행해서 재확인해도 좋습니다.

#### 모든 컴퓨터에서 스왑 메모리 (Swap Memory)를 비활성화

##### Step 1. `swapoff` 명령어로 스왑 메모리를 모두 비활성화

```bash
$ sudo swapoff -a
[sudo] password for k8smaster: 
$
```

##### Step 2. `/etc/fstab`파일의 swap관련 부분을 비활성화

`/etc/fstab`파일을 텍스트 에디터로 열어서, `/swapfile`로 시작하는 swap 관련 부분을 제거하기 위해 줄의 제일 앞에 #를 붙여줍니다.

```bash
$ sudo nano /etc/fstab
```

#####  수정 전

```bash
/swapfile                                 none            swap    sw              0       0
```

##### 수정 후

```bash
#/swapfile                                 none            swap    sw              0       0
```

## 마스터 설정: `kubeadm init`의 기본값으로 초기화 하기

`kubeadm init`를 실행할 때는 주의가 필요합니다. 왜냐하면 다시 실행하기 위해선 먼저 클러스터를 해체해야 하기 때문입니다. 상세한 내용은 쿠버네티스 공식 문서의 [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) > [tear down the cluster](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#tear-down)를 참고하세요.

#### Step 1. `$ sudo kubeadm init` 명령어 실행

```bash
$ sudo kubeadm init
```

##### `$ sudo kubeadm init` 명령어의 출력 메세지에 대한 설명

명령어를 실행하면 아래와 같은 메세지가 출력됩니다.

```bash
  ...
Your Kubernetes control-plane has initialized successfully!
  ...
$
```

> Your Kubernetes control-plane has initialized successfully!

의 앞부분은

* 쿠버네티스 설치 가능 여부를 사전 체크하고,
* 컨트롤 플레인 요소를 다운로드하고 설치한

결과가 출력됩니다. 설치를 진행하기에 문제가 있을 경우, 사전 체크 과정에서 warning이나 error를 출력하고 exit 됩니다. 

뒷부분은 클러스터 형성을 완료하기 위해 마스터와 노드에서 실행해야 하는 명령어를 보여줍니다.

##### 마스터에서

 `$HOME/.kube/config`를 설정하고

```bash
To start using your cluster, you need to run the following as a regular user:
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Pod Network를 추가합니다.

```bash
You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/
```

##### 노드에서

```bash
Then you can join any number of worker nodes by running the following on each as root:
kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

예를 들어

* `control-plane-host`가 `192.168.0.109`
* `control-plane-port`가 `6443`
* `token`이 `zqw1lb.tuhllf8m7zntibcq`
* `hash`가 `e3f15962b0535847add930d0e16fe92dc3e7ed139f29e0093e0b0766ca615671`

일 경우에 마지막 명령어는

```bash
kubeadm join 192.168.0.109:6443 --token zqw1lb.tuhllf8m7zntibcq \
    --discovery-token-ca-cert-hash sha256:e3f15962b0535847add930d0e16fe92dc3e7ed139f29e0093e0b0766ca615671
```

가 됩니다. **중요: 이 명령어를 잘 기록해야 합니다. 새 노드를 클러스터에 조인 (join)하기 위해서 필요합니다.** 

#### Step 2. `$HOME/.kube/config`를 설정

마스터에서 아래의 명령어를 실행합니다. 이것은 `$ sudo kubeadm init` 의 출력 결과에 있는 명령어와 동일합니다.

```bash
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

##### 명령어에 대한 설명

root 계정이 아닌 일반 사용자 계정으로 클러스터를 제어하기 위한 설정입니다. 제어를 위해선 `kubectl` 커맨드 명령어를 사용하게 됩니다.

일반 사용자 계정으로 `$HOME/.kube` 디렉토리를 만든 후, `/etc/kubernetes/admin.conf`의 내용을 `$HOME/.kube/config`으로 복사합니다. 마지막 명령어는 파일의 권한을 일반 사용자 계정으로 변경합니다. 이것이 없다면 파일을 쓰기 위해 루트 권한이 필요합니다.

```bash
$ cat config
cat: config: Permission denied
$
```

#### Step 3. Pod Network로 calico를 추가

```bash
$ kubectl apply -f [podnetwork].yaml
```

`podnetwork`로 기본인 calico를 선택할 경우에 아래 명령어를 실행합니다.

```bash
$ sudo kubectl apply -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
```

출력 메세지는 다음과 같습니다.

```bash
[sudo] password for k8smaster: 
configmap/calico-config created
customresourcedefinition.apiextensions.k8s.io/bgpconfigurations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/bgppeers.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/blockaffinities.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/clusterinformations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/felixconfigurations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/globalnetworkpolicies.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/globalnetworksets.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/hostendpoints.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamblocks.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamconfigs.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ipamhandles.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/ippools.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/kubecontrollersconfigurations.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/networkpolicies.crd.projectcalico.org created
customresourcedefinition.apiextensions.k8s.io/networksets.crd.projectcalico.org created
clusterrole.rbac.authorization.k8s.io/calico-kube-controllers created
clusterrolebinding.rbac.authorization.k8s.io/calico-kube-controllers created
clusterrole.rbac.authorization.k8s.io/calico-node created
clusterrolebinding.rbac.authorization.k8s.io/calico-node created
daemonset.apps/calico-node created
serviceaccount/calico-node created
deployment.apps/calico-kube-controllers created
serviceaccount/calico-kube-controllers created
$
```

다른 `podnetwork`을 선택할 경우의 명령어는 다음 파트에서 설명합니다.

#### Step 4. 클러스터 노드 정보를 확인

`kubectl get nodes`명령어로 클러스터 노드 정보를 확인해봅니다.

```bash
$ kubectl get nodes
NAME                    STATUS   ROLES    AGE   VERSION
k8smaster-gpu-desktop   Ready    master   4h    v1.18.5
$
```

현재로썬 마스터 하나만 있습니다.

## 노드 설정:  `kubeadm join`명령어로 클러스터에 조인 (join)하기

앞서 생성된 클러스터에 노드를 조인 (join) 하기 위해,   `kubeadm join`명령어를 실행합니다. 상세한 내용은 쿠버네티스 공식 문서의 [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) > [join nodes to your cluster](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/#join-nodes)를 참고하세요.

#### Step 1.  `kubeadm join`명령어 실행

`kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>` 에 해당하는 명령어를 실행합니다. 구체적인 파라미터 값은 마스터에서 `kubeadm init` 명령어 실행 시 출력됩니다. 예를 들면,

```bash
$ sudo kubeadm join 192.168.0.109:6443 --token zqw1lb.tuhllf8m7zntibcq \
    --discovery-token-ca-cert-hash sha256:e3f15962b0535847add930d0e16fe92dc3e7ed139f29e0093e0b0766ca615671
```

마스터와 노드의 상호 인증을 위해서 토큰이 사용됩니다. 이 토큰은 안전하게 잘 관리해야 하는데, 토큰이 있으면 누구나 클러스터에 노드를 붙일 수 있기 때문입니다. 토큰에 대한 조작은 `kubeadm token` 명령어로 할 수 있습니다. 상세한 내용은 쿠버네티스 공식 문서의 [kubeadm reference guide](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-token/)를 참고하세요. 

## 다음

* [kubeadm init args로  단일 구성 클러스터 생성하기](create_a_single_control_plane_cluster_with_kubeadm_init_args.md)

## 부록: `kubeadm init` 명령어 실행 시 연관있는 항목

 `kubeadm init` 명령어는 아래의 복잡한 항목을 간단히 설치해줍니다.

```text
preflight                    Run pre-flight checks
kubelet-start                Write kubelet settings and (re)start the kubelet
certs                        Certificate generation
  /ca                          Generate the self-signed Kubernetes CA to provision identities for other Kubernetes components
  /apiserver                   Generate the certificate for serving the Kubernetes API
  /apiserver-kubelet-client    Generate the certificate for the API server to connect to kubelet
  /front-proxy-ca              Generate the self-signed CA to provision identities for front proxy
  /front-proxy-client          Generate the certificate for the front proxy client
  /etcd-ca                     Generate the self-signed CA to provision identities for etcd
  /etcd-server                 Generate the certificate for serving etcd
  /etcd-peer                   Generate the certificate for etcd nodes to communicate with each other
  /etcd-healthcheck-client     Generate the certificate for liveness probes to healthcheck etcd
  /apiserver-etcd-client       Generate the certificate the apiserver uses to access etcd
  /sa                          Generate a private key for signing service account tokens along with its public key
kubeconfig                   Generate all kubeconfig files necessary to establish the control plane and the admin kubeconfig file
  /admin                       Generate a kubeconfig file for the admin to use and for kubeadm itself
  /kubelet                     Generate a kubeconfig file for the kubelet to use *only* for cluster bootstrapping purposes
  /controller-manager          Generate a kubeconfig file for the controller manager to use
  /scheduler                   Generate a kubeconfig file for the scheduler to use
control-plane                Generate all static Pod manifest files necessary to establish the control plane
  /apiserver                   Generates the kube-apiserver static Pod manifest
  /controller-manager          Generates the kube-controller-manager static Pod manifest
  /scheduler                   Generates the kube-scheduler static Pod manifest
etcd                         Generate static Pod manifest file for local etcd
  /local                       Generate the static Pod manifest file for a local, single-node local etcd instance
upload-config                Upload the kubeadm and kubelet configuration to a ConfigMap
  /kubeadm                     Upload the kubeadm ClusterConfiguration to a ConfigMap
  /kubelet                     Upload the kubelet component config to a ConfigMap
upload-certs                 Upload certificates to kubeadm-certs
mark-control-plane           Mark a node as a control-plane
bootstrap-token              Generates bootstrap tokens used to join a node to a cluster
kubelet-finalize             Updates settings relevant to the kubelet after TLS bootstrap
  /experimental-cert-rotation  Enable kubelet client certificate rotation
addon                        Install required addons for passing Conformance tests
  /coredns                     Install the CoreDNS addon to a Kubernetes cluster
  /kube-proxy                  Install the kube-proxy addon to a Kubernetes cluster
```

참고로 이 중 컨트롤 플레인과 etcd에 해당하는 부분은 아래와 같습니다.

```text
control-plane
  /apiserver
  /controller-manager
  /scheduler
etcd
  /local
```

## 부록: `sudo kubeadm init`명령어의 전체 메세지

```bash
$ sudo kubeadm init
[sudo] password for k8smaster: 
W0703 14:55:49.388649   10153 configset.go:202] WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
[init] Using Kubernetes version: v1.18.5
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [k8smaster-gpu-desktop kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.0.109]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [k8smaster-gpu-desktop localhost] and IPs [192.168.0.109 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [k8smaster-gpu-desktop localhost] and IPs [192.168.0.109 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
W0703 14:57:09.900821   10153 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[control-plane] Creating static Pod manifest for "kube-scheduler"
W0703 14:57:09.901429   10153 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 20.002615 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node k8smaster-gpu-desktop as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node k8smaster-gpu-desktop as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: zqw1lb.tuhllf8m7zntibcq
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.0.109:6443 --token zqw1lb.tuhllf8m7zntibcq \
    --discovery-token-ca-cert-hash sha256:e3f15962b0535847add930d0e16fe92dc3e7ed139f29e0093e0b0766ca615671
$
```