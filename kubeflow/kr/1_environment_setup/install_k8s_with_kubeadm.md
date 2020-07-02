* Draft: 2020-07-01 (Wed)

### kubeadm 을 이용한 쿠버네티스 설치

이 부분은 쿠버네티스 공식 문서의 [kubeadm으로 클러스터 구성하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/) 혹은 [Bootstrapping clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/)에 해당합니다. 

* kubeadm 설치하기 / [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

* 클러스터 설정하기
  * kubeadm로 단일 컨트롤 플레인 클러스터 설정하기 / [Creating a single control-plane cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)
  * [kubeadm로 컨트롤 플레인 사용자 정의하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/control-plane-flags/) / [Customizing control plane configuration with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/control-plane-flags/)
  * kubeadm로 클러스터의 각 kubelet 설정하기 / [Configuring each kubelet in your cluster using kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/kubelet-integration/)

## kubeadm 설치하기

아래는  [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)에서 해당하는 내용입니다.

[kubeadm 설치 전 사전 확인 작업](verify_before_installing_k8s.md)

[kubeadm 설치하기](install_kubeadm.md)







##### [턴키 클라우드 솔루션](https://kubernetes.io/ko/docs/setup/production-environment/turnkey/)