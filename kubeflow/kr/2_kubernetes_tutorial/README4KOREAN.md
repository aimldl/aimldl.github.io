* Draft: 2020-07-28 (Tue)

# [쿠버네티스 문서](https://kubernetes.io/ko/docs/home/) (Kubernetes Tutorial) - 한국어 버전 (in Korean)
##  목차
작성일: 2020-07-28 (Tue)
* [문서 / 시작하기](https://kubernetes.io/ko/docs/setup/)
  * [릴리스 노트와 버전 차이 지원(skew)](https://kubernetes.io/ko/docs/setup/release/)
    * [v1.18 릴리스 노트](https://kubernetes.io/ko/docs/setup/release/notes/)
  * [학습 환경](https://kubernetes.io/ko/docs/setup/learning-environment/)
    * [Minikube로 쿠버네티스 설치](https://kubernetes.io/ko/docs/setup/learning-environment/minikube/)
  * [운영 환경](https://kubernetes.io/ko/docs/setup/production-environment/)
    * [컨테이너 런타임](https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/)
    * [Installing Kubernetes with deployment tools](https://kubernetes.io/ko/docs/setup/production-environment/tools/)
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
  * [도구 설치](https://kubernetes.io/ko/docs/tasks/tools/) 컴퓨터에서 쿠버네티스 도구를 설정한다.
    * [kubectl 설치 및 설정](https://kubernetes.io/ko/docs/tasks/tools/install-kubectl/)
    * [Minikube 설치](https://kubernetes.io/ko/docs/tasks/tools/install-minikube/)
  * [클러스터 운영](https://kubernetes.io/ko/docs/tasks/administer-cluster/) 클러스터를 운영하기 위한 공통 태스크를 배운다.
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
    * [DNS 서비스 사용자 정의하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/dns-custom-nameservers/)
    * [고가용성 쿠버네티스 클러스터 마스터 설정하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/highly-available-master/)
    * [기본 스토리지클래스(StorageClass) 변경하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/change-default-storage-class/)
    * [네트워크 폴리시(Network Policy) 선언하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/declare-network-policy/)
    * [노드에 대한 확장 리소스 알리기](https://kubernetes.io/ko/docs/tasks/administer-cluster/extended-resource-node/)
    * [서비스 디스커버리를 위해 CoreDNS 사용하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/coredns/)
    * [쿠버네티스 API를 사용하여 클러스터에 접근하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/access-cluster-api/)
    * [클러스터 관리](https://kubernetes.io/ko/docs/tasks/administer-cluster/cluster-management/)
    * [클러스터에서 실행되는 서비스에 접근](https://kubernetes.io/ko/docs/tasks/administer-cluster/access-cluster-services/)
    * [퍼시스턴트볼륨 반환 정책 변경하기](https://kubernetes.io/ko/docs/tasks/administer-cluster/change-pv-reclaim-policy/)
  * [파드와 컨테이너 설정](https://kubernetes.io/ko/docs/tasks/configure-pod-container/) 파드와 컨테이너에 대한 공통 구성 태스크들을 수행한다.
  * [쿠버네티스 오브젝트 관리](https://kubernetes.io/ko/docs/tasks/manage-kubernetes-objects/) 쿠버네티스 API와 상호 작용하기 위한 선언적이고 명령적인 패러다임
  * [애플리케이션에 데이터 주입하기](https://kubernetes.io/ko/docs/tasks/inject-data-application/) 워크로드를 실행하는 파드에 대한 구성과 기타 데이터를 지정한다.
  * [애플리케이션 실행](https://kubernetes.io/ko/docs/tasks/run-application/) 스테이트리스와 스테이트풀 애플리케이션 모두를 실행하고 관리한다.
  * [클러스터 내 어플리케이션 액세스](https://kubernetes.io/ko/docs/tasks/access-application-cluster/) 클러스터의 애플리케이션에 접근하기 위해 로드 밸런싱, 포트 포워딩, 방화벽 설정 또는 DNS 구성을 설정한다
  * [모니터링, 로깅, 그리고 디버깅](https://kubernetes.io/ko/docs/tasks/debug-application-cluster/) 모니터링 및 로깅을 설정하여 클러스터 문제를 해결하거나, 컨테이너화된 애플리케이션을 디버깅한다.
  * [TLS](https://kubernetes.io/ko/docs/tasks/tls/) TLS(Transport Layer Security)를 사용하여 클러스터 내 트래픽을 보호하는 방법을 이해한다.
  * [클러스터 데몬 관리](https://kubernetes.io/ko/docs/tasks/manage-daemon/) 롤링 업데이트 수행과 같은 데몬셋 관리를 위한 일반적인 작업을 수행한다.
  * [네트워킹](https://kubernetes.io/ko/docs/tasks/network/) 클러스터에 대한 네트워킹 설정 방법에 대해 배운다.
  * [GPU 스케줄링](https://kubernetes.io/ko/docs/tasks/manage-gpus/scheduling-gpus/) 클러스터의 노드별로 리소스로 사용할 GPU를 구성하고 스케줄링한다.
  * [HugePages 관리](https://kubernetes.io/ko/docs/tasks/manage-hugepages/scheduling-hugepages/) 클러스터에서 huge page를 스케줄할 수 있는 리소스로 구성하고 관리한다.
  * [플러그인으로 kubectl 확장](https://kubernetes.io/ko/docs/tasks/extend-kubectl/kubectl-plugins/) kubectl 플러그인을 작성하고 설치해서 kubectl을 확장한다.
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
