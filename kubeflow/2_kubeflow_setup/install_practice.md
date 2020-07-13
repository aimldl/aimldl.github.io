* Draft: 2020-07-13 (Mon)

# Kubeflow 설정 



```bash
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.4", GitCommit:"c96aede7b5205121079932896c4ad89bb93260af", GitTreeState:"clean", BuildDate:"2020-06-17T11:41:22Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.5", GitCommit:"e6503f8d8f769ace2f338794c914a96fc335df0f", GitTreeState:"clean", BuildDate:"2020-06-26T03:39:24Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
$
```

쿠버네티스 버전 1.18이 설치 되어 있습니다.

```bash
Client Version: version.Info{Major:"1", Minor:"18"
Server Version: version.Info{Major:"1", Minor:"18"
```

하지만 이 버전은 Kubeflow와 호환이 되지 않습니다. 쿠버네티스와 쿠브플로우의 버전은 아래 표에 정리되어 있습니다. 

> The recommended Kubernetes version is 1.14. Kubeflow has been validated and tested on Kubernetes 1.14.
>
> - Your cluster must run at least Kubernetes version 1.11.
> - Kubeflow **does not work** on Kubernetes 1.16.
> - Older versions of Kubernetes may not be compatible with the latest Kubeflow versions. The following matrix provides information about compatibility between Kubeflow and Kubernetes versions.

> | Kubernetes Versions | Kubeflow 0.4   | Kubeflow 0.5   | Kubeflow 0.6   | Kubeflow 0.7   | Kubeflow 1.0        |
> | ------------------- | -------------- | -------------- | -------------- | -------------- | ------------------- |
> | 1.11                | **compatible** | **compatible** | incompatible   | incompatible   | incompatible        |
> | 1.12                | **compatible** | **compatible** | incompatible   | incompatible   | incompatible        |
> | 1.13                | **compatible** | **compatible** | incompatible   | incompatible   | incompatible        |
> | 1.14                | **compatible** | **compatible** | **compatible** | **compatible** | **compatible**      |
> | 1.15                | incompatible   | **compatible** | **compatible** | **compatible** | **compatible**      |
> | 1.16                | incompatible   | incompatible   | incompatible   | incompatible   | **no known issues** |
> | 1.17                | incompatible   | incompatible   | incompatible   | incompatible   | **no known issues** |
> | 1.18                | incompatible   | incompatible   | incompatible   | incompatible   | **no known issues** |
>
> - **incompatible**: the combination does not work at all
> - **compatible**: all Kubeflow features have been tested and verified for the Kubernetes version
> - **no known issues**: the combination has not been fully tested but there are no repoted issues
>
> 출처: [ Overview of Deployment on Existing Clusters > Minimum system requirements](https://www.kubeflow.org/docs/started/k8s/overview/#minimum-system-requirements)

쿠버네티스 1.14를 추천하므로 쿠버네티스 재설치를 진행합니다.



## ubeadm, kubelet, kubectl 설치하기

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



Google search: uninstall kubernetes

[Kubernetes completely uninstall](https://medium.com/@meysam1369/kubernetes-completely-uninstall-3f2a83dd985d), 2018-08-07, Medium

```bash
$ sudo -i
[sudo] password for k8smaster: 
root@k8smaster-gpu-desktop:~# kubeadm reset
[reset] Reading configuration from the cluster...
#
```

If the cluster is node, First delete it from master

```bash
# kubectl drain <node name> — delete-local-data — force — ignore-daemonsets
# kubectl delete node <node name>
```

> Then remove **kubeadm** completely
>
> ```bash
> kubeadm reset 
> # on debian base 
> sudo apt-get purge kubeadm kubectl kubelet kubernetes-cni kube* 
> #on centos base
> sudo yum remove kubeadm kubectl kubelet kubernetes-cni kube*# on debian base
> sudo apt-get autoremove
> #on centos base
> sudo yum autoremove
>  
> sudo rm -rf ~/.kube
> ```

```bash
# kubeadm reset
# apt-get purge kubeadm kubectl kubelet kubernetes-cni kube*
  ...
# apt-get autoremove
# rm -rf ~/.kube
```



```bash
# kubeadm reset
[reset] Reading configuration from the cluster...
[reset] FYI: You can look at this config file with 'kubectl -n kube-system get cm kubeadm-config -oyaml'
[reset] WARNING: Changes made to this host by 'kubeadm init' or 'kubeadm join' will be reverted.
[reset] Are you sure you want to proceed? [y/N]: y
[preflight] Running pre-flight checks
[reset] Removing info for node "k8smaster-gpu-desktop" from the ConfigMap "kubeadm-config" in the "kube-system" Namespace
{"level":"warn","ts":"2020-07-13T17:16:12.214+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:12.269+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:12.380+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:12.594+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:13.013+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:13.849+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:15.561+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:18.783+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:25.285+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:16:38.210+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
{"level":"warn","ts":"2020-07-13T17:17:04.582+0900","caller":"clientv3/retry_interceptor.go:61","msg":"retrying of unary invoker failed","target":"endpoint://client-f2d8c4d4-b080-4b76-a4e4-67d56576d2ac/192.168.0.109:2379","attempt":0,"error":"rpc error: code = Unknown desc = etcdserver: re-configuration failed due to not enough started members"}
W0713 17:17:04.583134     830 removeetcdmember.go:61] [reset] failed to remove etcd member: etcdserver: re-configuration failed due to not enough started members
.Please manually remove this etcd member using etcdctl
[reset] Stopping the kubelet service
[reset] Unmounting mounted directories in "/var/lib/kubelet"
[reset] Deleting contents of config directories: [/etc/kubernetes/manifests /etc/kubernetes/pki]
[reset] Deleting files: [/etc/kubernetes/admin.conf /etc/kubernetes/kubelet.conf /etc/kubernetes/bootstrap-kubelet.conf /etc/kubernetes/controller-manager.conf /etc/kubernetes/scheduler.conf]
[reset] Deleting contents of stateful directories: [/var/lib/etcd /var/lib/kubelet /var/lib/dockershim /var/run/kubernetes /var/lib/cni]

The reset process does not clean CNI configuration. To do so, you must remove /etc/cni/net.d

The reset process does not reset or clean up iptables rules or IPVS tables.
If you wish to reset iptables, you must do so manually by using the "iptables" command.

If your cluster was setup to utilize IPVS, run ipvsadm --clear (or similar)
to reset your system's IPVS tables.

The reset process does not clean your kubeconfig files and you must remove them manually.
Please, check the contents of the $HOME/.kube/config file.

#
```

