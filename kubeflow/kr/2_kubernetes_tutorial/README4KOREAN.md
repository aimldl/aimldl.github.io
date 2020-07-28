* 

# 쿠버네티스 문서 (Kubernetes Tutorial) - 한국어 버전 (in Korean)

## [쿠버네티스 문서](https://kubernetes.io/ko/docs/home/) 목차
* [문서 / 시작하기](https://kubernetes.io/ko/docs/setup/)
  * [릴리스 노트와 버전 차이 지원(skew)](https://kubernetes.io/ko/docs/setup/release/)
    * [v1.18 릴리스 노트](https://kubernetes.io/ko/docs/setup/release/notes/)
  * [학습 환경](https://kubernetes.io/ko/docs/setup/learning-environment/)
    * [Minikube로 쿠버네티스 설치](https://kubernetes.io/ko/docs/setup/learning-environment/minikube/)
  * [운영 환경](https://kubernetes.io/ko/docs/setup/production-environment/)
    * [컨테이너 런타임](https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/)
    * [Installing Kubernetes with deployment tools]
      * [kubeadm으로 클러스터 구성하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/)
        * [kubeadm으로 컨트롤 플레인 사용자 정의하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/control-plane-flags/)
        * [고가용성 토폴로지 선택](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/ha-topology/)
      * [Kops로 쿠버네티스 설치하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kops/)
    * [턴키 클라우드 솔루션](https://kubernetes.io/ko/docs/setup/production-environment/turnkey/) (내용 무)
    * [온-프레미스 VM](https://kubernetes.io/ko/docs/setup/production-environment/on-premises-vm/) (내용 무)
    * [쿠버네티스에서 윈도우](https://kubernetes.io/ko/docs/setup/production-environment/windows/)
      * [쿠버네티스에서 윈도우 컨테이너 스케줄링을 위한 가이드](https://kubernetes.io/ko/docs/setup/production-environment/windows/user-guide-windows-containers/)
  * [kubeadm으로 컨트롤 플레인 사용자 정의하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/control-plane-flags/)
  * [Kops로 쿠버네티스 설치하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kops/)
  * [쿠버네티스에서 윈도우 컨테이너 스케줄링을 위한 가이드](https://kubernetes.io/ko/docs/setup/production-environment/windows/user-guide-windows-containers/)
  * [모범 사례](https://kubernetes.io/ko/docs/setup/best-practices/)
    * [여러 영역에서 구동](https://kubernetes.io/ko/docs/setup/best-practices/multiple-zones/)
    * [대형 클러스터 구축](https://kubernetes.io/ko/docs/setup/best-practices/cluster-large/)
    * [PKI 인증서 및 요구 조건](https://kubernetes.io/ko/docs/setup/best-practices/certificates/)
* [문서 / 개념](https://kubernetes.io/ko/docs/concepts/)
* [문서 / 태스크](https://kubernetes.io/ko/docs/tasks/)
[문서 / 태스크 / 클러스터 운영](https://kubernetes.io/ko/docs/tasks/administer-cluster/)
클러스터를 운영하기 위한 공통 태스크를 배운다.
  * [kubeadm으로 관리하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/kubeadm/)
    * [kubeadm을 사용한 인증서 관리](https://kubernetes.io/ko/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/)
    * [kubeadm 클러스터 업그레이드](https://kubernetes.io/ko/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)
    * [윈도우 노드 추가](https://kubernetes.io/ko/docs/tasks/administer-cluster/kubeadm/adding-windows-nodes/)
    * [윈도우 노드 업그레이드](https://kubernetes.io/ko/docs/tasks/administer-cluster/kubeadm/upgrading-windows-nodes/)

  * [메모리, CPU 와 API 리소스 관리](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/)
    * [네임스페이스에 대한 기본 메모리 요청량과 상한 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/)
    * [네임스페이스에 대한 기본 CPU 요청량과 상한 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/cpu-default-namespace/)
    * [네임스페이스에 대한 메모리의 최소 및 최대 제약 조건 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/memory-constraint-namespace/)
    * [네임스페이스에 대한 CPU의 최소 및 최대 제약 조건 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/cpu-constraint-namespace/)
    * [네임스페이스에 대한 메모리 및 CPU 쿼터 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/)
    * [네임스페이스에 대한 파드 쿼터 구성](https://kubernetes.io/ko/docs/tasks/administer-cluster/manage-resources/quota-pod-namespace/)
  * [네트워크 폴리시 제공자(Network Policy Provider) 설치](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/)
    * [네트워크 폴리시로 캘리코(Calico) 사용하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/calico-network-policy/)
    * [네트워크 폴리시로 실리움(Cilium) 사용하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/cilium-network-policy/)
    * [네트워크 폴리시로 큐브 라우터(Kube-router) 사용하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/kube-router-network-policy/)
    * [네트워크 폴리시로 로마나(Romana)](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/romana-network-policy/)
    * [네트워크 폴리시로 위브넷(Weave Net) 사용하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/network-policy-provider/weave-network-policy/)
  * [DNS 서비스 사용자 정의하기]

  * [고가용성 쿠버네티스 클러스터 마스터 설정하기]

  * [기본 스토리지클래스(StorageClass) 변경하기]

  * [네트워크 폴리시(Network Policy) 선언하기]

  * [노드에 대한 확장 리소스 알리기]

  * [서비스 디스커버리를 위해 CoreDNS 사용하기]

  * [쿠버네티스 API를 사용하여 클러스터에 접근하기]

  * [클러스터 관리]

  * [클러스터에서 실행되는 서비스에 접근]

  * [퍼시스턴트볼륨 반환 정책 변경하기]

* [문서 / 튜토리얼](https://kubernetes.io/ko/docs/tutorials/)
* [문서 / 레퍼런스](https://kubernetes.io/ko/docs/reference/)
* [문서 / 쿠버네티스 문서에 기여하기](https://kubernetes.io/ko/docs/contribute/)

## 읽을 부분
[쿠버네티스 문서](https://kubernetes.io/ko/docs/home/)
* [문서 / 시작하기](https://kubernetes.io/ko/docs/setup/)
  * [kubeadm으로 컨트롤 플레인 사용자 정의하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/control-plane-flags/)
  * [Kops로 쿠버네티스 설치하기](https://kubernetes.io/ko/docs/setup/production-environment/tools/kops/)
  * [쿠버네티스에서 윈도우 컨테이너 스케줄링을 위한 가이드](https://kubernetes.io/ko/docs/setup/production-environment/windows/user-guide-windows-containers/)
  * [모범 사례](https://kubernetes.io/ko/docs/setup/best-practices/)
    * [여러 영역에서 구동](https://kubernetes.io/ko/docs/setup/best-practices/multiple-zones/)
    * [대형 클러스터 구축](https://kubernetes.io/ko/docs/setup/best-practices/cluster-large/)
    * [PKI 인증서 및 요구 조건](https://kubernetes.io/ko/docs/setup/best-practices/certificates/)
