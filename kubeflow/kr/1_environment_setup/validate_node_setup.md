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
