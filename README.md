# XecureDB intall

## windows 

특이사항 없음.

## LINUX

### 1. linux VM 설치
![image](https://github.com/auspicious0/XecureDB/assets/108572025/d7afd97b-6243-41bf-9c1f-11fa4539e280)

### 2. 방화벽 해제

```
systemctl status firewalld
systemctl stop firewalld
systemctl status firewalld inactive #확인
```

### 3. SELINUX = disabled 설정

```
cd /etc/selinux/
vi config
su –
cd etc/selinux
vi config  -> SELINUX=disabled
reboot
```

### 4. 리눅스 환경 변수 설정 방법 정리

```
#우선 z_package가 담긴 그룹 아래에서 설정한다.
vi ~/.bash_profile #들어간 후 export LD_LIBRARY_PATH = 위치값 1: 위치값 2 와같은 형식으로 환경 변수 입력
source ~/.bash_profile #환경 변수 등록
env | grep LD_ #최종 확인 
```

![image](https://github.com/auspicious0/XecureDB/assets/108572025/8f56163d-87b8-403e-b00a-bc89d39b9c3c)

### 5. 로컬 작업 파일을 리눅스에 등록하기

```
#drag n drop
tar zxvf #파일명 (압축풀기)

```

## 오류사항

### 1. ip가 제대로 반영이 되어 있지 않을 때

```
su
cd /etc/sysconfig/network-scripts/
vi ifcfg-enp0s3 #BOOTPROTO 를 “none”으로 수정
systemctl restart network #(네트워크 재시작) 
ifconfig #이더넷 확인

```
### 2. 권한 생성이 제대로 되어 있지 않을 때

권한 생성이란?

파일생성 chmod 000 test(유저, 그룹, other) 

ex )권한이 7 이라면 읽고 쓰고 실행 가능 (4 - read, 2 – write, 1-실행) 

따라서 생성된 파일은 유저, 그룹, other 모두 아무런 권한이 없다.

ex )유저는 읽고 실행 가능, 그룹은 읽기 가능, others는 전부 가능하게 하려면 -> 

chmod 547 test


### 3. 디렉터리의 소유자를 변경하고자 할 때

chown(change owner) 를 사용한다.

ex) sudo chown alphabit::jcshin file.txt


### 4. 파일을 옮기고자 할 때

```
ls
mv *.key ../etc/ 
mv *.sf ../etc 
```
### 5. 윈도우 파일을 열 때

```
vi –b XDServer.CF
#\m을 모두 지워준다.
#	다시 실행 
```

### 6. 서버 실행 확인시

```
netstat –an | grep 932 # 포트확인
ps –ef | grep XDS 프로세스 확인
```

### 7. 연결 확인

ip port timeout 입력을 통해 확인 가능하다. 이렇게 만들면 data에 내용이 생성된다

## 일련의 동작에 대한 정리

비밀번호나 주민번호 등 보호해야할 정보를 암호화하기 위해서 하는 동작들이다.

암호화를 하는 툴이 바로  XecureDB이다. 암호화 복호화시 정해진 툴이 있는 것은 아니다. 사이트 별로 다르다.

아래는 메니저와 서버, api가 소통하는 과정에 대한 설명이다. 

메니저는 윈도우로 고정되어 있고 이와 소통하기 위한 서버는 리눅스 or 윈도우로 생성이 가능하다.

또한 api 역시 linux or windows로 생성이 가능하다.


