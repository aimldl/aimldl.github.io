* Draft: 2020-07-13 (Mon)

# Kubeflow 설정 

## 마스터 설정

마스터로 사용할 컴퓨터를 설정해봅니다.

## 신규 계정 만들기

쿠버네티스 전용으로 사용할 계정과 패스워드를 생성합니다. 

 Step 1. 새로운 컴퓨터의 기존 계정에 로그인합니다.

Step 2. 터미널을 열고, `adduser` 명령어에 신규 계정의 이름을 입력합니다. 여기에선 k8smaster를 계정 이름으로 씁니다. k8s는 Kubernetes의 축약어입니다.

```bash
$ sudo adduser k8smaster
```

현재 계정의 패스워드를 입력하고

```bash
[sudo] password for aimldl: 
Adding user `k8smaster' ...
Adding new group `k8smaster' (1002) ...
Adding new user `k8smaster' (1002) with group `k8smaster' ...
Creating home directory `/home/k8smaster' ...
Copying files from `/etc/skel' ...
```

 신규 생성할 계정의 패스워드를 입력합니다.

```bash
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for k8smaster
Enter the new value, or press ENTER for the default
	Full Name []: 
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
Is the information correct? [Y/n] y
$
```

Step 3. 기존 계정을 로그 아웃합니다.

Step 4. 새로 만들 계정과 패스워드를 써서 다시 로그인합니다.

새로운 환경이 만들어졌습니다.



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

## 





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

# 