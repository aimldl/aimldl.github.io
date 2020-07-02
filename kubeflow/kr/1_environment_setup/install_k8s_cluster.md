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

## 다음

* [컨테이너 런타임 (Container Runtime) 설치하기](install_container_runtime.md)
