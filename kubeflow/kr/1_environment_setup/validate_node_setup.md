* 2020-07-09 (Thu)
# 클러스터에 붙은 노드 구성 검증하기

```bash
$ sudo docker run -it --rm --privileged --net=host -v /:/rootfs -v $CONFIG_DIR:$CONFIG_DIR -v $LOG_DIR:/var/result k8s.gcr.io/node-test:0.2
```

```bash
$ sudo docker run -it --rm --privileged --net=host -v /:/rootfs -v $CONFIG_DIR:$CONFIG_DIR -v $LOG_DIR:/var/result k8s.gcr.io/node-test:0.2
Unable to find image 'k8s.gcr.io/node-test:0.2' locally
0.2: Pulling from node-test
43c265008fae: Pull complete 
a3ed95caeb02: Pull complete 
a55c87cb1c33: Pull complete 
56929588bea5: Pull complete 
Digest: sha256:18943086438949f8574d84a8f5cd32ec3e5607fb3a5e9100161373a46dc63ab3
Status: Downloaded newer image for k8s.gcr.io/node-test:0.2
Running Suite: E2eNode Suite
============================
Random Seed: 1594279385 - Will randomize all specs
Will run 88 of 162 specs

Running in parallel across 8 nodes

OS: Linux
KERNEL_VERSION: 4.15.0-108-generic
CONFIG_NAMESPACES: enabled
CONFIG_NET_NS: enabled
CONFIG_PID_NS: enabled
CONFIG_IPC_NS: enabled
CONFIG_UTS_NS: enabled
CONFIG_CGROUPS: enabled
CONFIG_CGROUP_CPUACCT: enabled
CONFIG_CGROUP_DEVICE: enabled
CONFIG_CGROUP_FREEZER: enabled
CONFIG_CGROUP_SCHED: enabled
CONFIG_CPUSETS: enabled
CONFIG_MEMCG: enabled
CONFIG_INET: enabled
CONFIG_EXT4_FS: enabled
CONFIG_PROC_FS: enabled
CONFIG_NETFILTER_XT_TARGET_REDIRECT: enabled (as module)
CONFIG_NETFILTER_XT_MATCH_COMMENT: enabled (as module)
CONFIG_OVERLAY_FS: enabled (as module)
CONFIG_AUFS_FS: enabled (as module)
CONFIG_BLK_DEV_DM: enabled
CGROUPS_CPU: enabled
CGROUPS_CPUACCT: enabled
CGROUPS_CPUSET: enabled
CGROUPS_DEVICES: enabled
CGROUPS_FREEZER: enabled
CGROUPS_MEMORY: enabled
DOCKER_VERSION: 19.03.12
F0709 16:23:05.757598     155 e2e_node_suite_test.go:96] system validation failed: unsupported docker version: 19.03.12


Failure [0.135 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  system validation
  Expected success, but got an error:
      <*errors.errorString | 0xc420292050>: {
          s: "system validation failed: exit status 1",
      }
      system validation failed: exit status 1

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:122
------------------------------
Failure [0.151 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.151 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.151 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.152 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.151 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.151 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------
Failure [0.153 seconds]
[BeforeSuite] BeforeSuite 
/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157

  BeforeSuite on Node 1 failed

  /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/test/e2e_node/e2e_node_suite_test.go:157
------------------------------

Ran 88 of 162 Specs in 0.239 seconds
FAIL! -- 0 Passed | 88 Failed | 0 Pending | 74 Skipped 

Ginkgo ran 1 suite in 403.927172ms
Test Suite Failed
$
```

Google search: kubernetes system validation failed: unsupported docker version

You need to downgrade docker to 18.06, until 18.09 is validated and supported by kubeadm:

https://github.com/kubernetes/kubernetes/blob/master/cmd/kubeadm/app/util/system/docker_validator.go#L41

It was only recently that kubeadm started to support anything beyond version 17.03: #3223

Apparently you are also missing other binaries, such as socat and maybe also crictl...

```
Removing the old version with :
sudo apt-get purge docker-ce
sudo rm -rf /var/lib/docker

And then reinstall as @afbjorklund said :

apt-get update && apt-get install docker-ce=18.06.0~ce~3-0~ubuntu
```

[v1.18 릴리스 노트](https://kubernetes.io/ko/docs/setup/release/notes/)

[Kubernetes version and version skew support policy](https://kubernetes.io/docs/setup/release/version-skew-policy/)

[Container runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

Version 19.03.11 is recommended, but 1.13.1, 17.03, 17.06, 17.09, 18.06 and 18.09 are known to work as well. 

내 버전은 하나 높은 19.03.12이므로 다운 그레이드 해줘야 함.
버전 확인
```bash
$ docker version
Client: Docker Engine - Community
 Version:           19.03.12
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        48a66213fe
 Built:             Mon Jun 22 15:45:36 2020
 OS/Arch:           linux/amd64
 Experimental:      false
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/version: dial unix /var/run/docker.sock: connect: permission denied
$
```

Docker 제거하기
```bash
$ dpkg -l | grep -i docker
ii  docker-ce                                  5:19.03.12~3-0~ubuntu-bionic                     amd64        Docker: the open-source application container engine
ii  docker-ce-cli                              5:19.03.12~3-0~ubuntu-bionic                     amd64        Docker CLI: the open-source application container engine
$ sudo apt-get purge -y docker-engine docker docker.io docker-ce
  ...
Package 'docker' is not installed, so not removed
Package 'docker.io' is not installed, so not removed
Package 'docker-engine' is not installed, so not removed
The following packages were automatically installed and are no longer required:
  aufs-tools cgroupfs-mount pigz
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  ...
$ sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce
  ...
Package 'docker' is not installed, so not removed
Package 'docker.io' is not installed, so not removed
Package 'docker-ce' is not installed, so not removed
Package 'docker-engine' is not installed, so not removed
The following packages will be REMOVED:
  aufs-tools* cgroupfs-mount* pigz*
  ...
$
```
참고: [Uninstall Docker]()


설치하기
[ Container runtimes > Docker](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#docker)

다운 그레이드 한 버전을 설치했지만,
```bash
# docker version
Client: Docker Engine - Community
 Version:           19.03.12
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        48a66213fe
 Built:             Mon Jun 22 15:45:36 2020
 OS/Arch:           linux/amd64
 Experimental:      false
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
#
```
버전에 문제가 있음. 공식 문서의 명령어를 썼지만 안 됨.

```bash
# apt-cache madison docker-ce
 docker-ce | 5:19.03.12~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.11~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.10~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.9~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.8~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.7~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.6~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:19.03.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.9~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.8~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.7~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.6~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 5:18.09.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.3~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.2~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.1~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.06.0~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
 docker-ce | 18.03.1~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
#
```
b. Install a specific version using the version string from the second column, for example, 5:18.09.1~3-0~ubuntu-xenial.

$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io

Version 19.03.11 is recommended, but 1.13.1, 17.03, 17.06, 17.09, 18.06 and 18.09 

docker-ce | 5:19.03.11~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
  ...
docker-ce | 5:18.09.9~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.8~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.7~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.6~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.5~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.4~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.3~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.2~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.1~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 5:18.09.0~3-0~ubuntu-bionic | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 18.06.3~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 18.06.2~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 18.06.1~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages
docker-ce | 18.06.0~ce~3-0~ubuntu | https://download.docker.com/linux/ubuntu bionic/stable amd64 Packages

19.03.11, 18.09, 18.06 만 보여지고 1.13.1, 17.03, 17.06, 17.09는 없음.

<VERSION_STRING> = 5:19.03.11~3-0~ubuntu-bionic
```bash
$ sudo apt-get install docker-ce=5:19.03.11~3-0~ubuntu-bionic docker-ce-cli=5:19.03.11~3-0~ubuntu-bionic containerd.io
```

```bash
$ apt-get install docker-ce=5:19.03.11~3-0~ubuntu-bionic docker-ce-cli=5:19.03.11~3-0~ubuntu-bionic containerd.io
Reading package lists... Done
Building dependency tree       
Reading state information... Done
containerd.io is already the newest version (1.2.13-2).
The following additional packages will be installed:
  aufs-tools cgroupfs-mount pigz
The following NEW packages will be installed:
  aufs-tools cgroupfs-mount docker-ce pigz
The following packages will be DOWNGRADED:
  docker-ce-cli
0 upgraded, 4 newly installed, 1 downgraded, 0 to remove and 80 not upgraded.
Need to get 63.9 MB of archives.
After this operation, 107 MB of additional disk space will be used.
Do you want to continue? [Y/n] 
  ...
$
```
```bash
# docker version
Client: Docker Engine - Community
 Version:           19.03.11
 API version:       1.40
 Go version:        go1.13.10
 Git commit:        42e35e61f3
 Built:             Mon Jun  1 09:12:22 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.11
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.10
  Git commit:       42e35e61f3
  Built:            Mon Jun  1 09:10:54 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.2.13
  GitCommit:        7ad184331fa3e55e52b890ea95e65ba581ae3429
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
#
```
맞는 버전이 설치 됨.

# lsb_release -cs
bionic

apt-get install docker-ce=5:19.03.11~3-0~ubuntu-bionic docker-ce-cli=5:19.03.11~3-0~ubuntu-bionic containerd.io

Uninstall
```bash
$ sudo apt-get purge docker-ce docker-ce-cli containerd.io
$ sudo rm -rf /var/lib/docker
```
제거 확인
```bash
$ docker version
-bash: /usr/bin/docker: No such file or directory
$
```
```bash
$ apt-get install docker-ce=5:19.03.11~3-0~ubuntu-bionic docker-ce-cli=5:19.03.11~3-0~ubuntu-bionic containerd.io=1.2.13-2
```
버전을 확인합니다.
```bash
$ docker version
Client: Docker Engine - Community
 Version:           19.03.11
  ...
Server: Docker Engine - Community
 Engine:
  Version:          19.03.11
  ...
containerd:
  Version:          1.2.13
  ...
$
```
모두 원하는 버전이 설치되었습니다

노드 테스트는 여전히 실패가 뜹니다.
Google search: kubernetes Node Conformance Test system validation failed: unsupported docker version: 19.03.11

[Node conformance test NodeProblemDetector failed against all docker ce and ee versions from 17.06.--19.03](https://github.com/kubernetes/kubernetes/issues/78186)

 이 글을 보면 모든 Docker 버전에 대해 테스트 했지만 실패했다고 되어 있습니다.
 
 검색 결과가 몇 개 나오지 않아서 검색 범위를 넖혀 봅니다.
 Google search: kubernetes Node Conformance Test system validation failed: unsupported docker version: 19.03.11
 
 유용한 정보는 찾을 수 없습니다.
 
