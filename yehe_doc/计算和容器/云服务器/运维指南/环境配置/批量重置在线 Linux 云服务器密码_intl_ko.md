## 작업 시나리오

본 문서는 비 종료 상태에서 여러 Linux 시스템 CVM의 비밀번호 일괄 재설정 관련 작업에 대해 소개합니다.

## 스크립트 다운로드
Tencent Cloud는 재설정 작업을 할 스크립트를 작성해두었기에, 해당 재설정 스크립트를 CVM에 다운로드 및 압축 해제하면 편리하게 온라인에서 일괄 재설정할 수 있습니다.
획득 경로: `http://batchchpasswd-10016717.file.myqcloud.com/batch-chpasswd.tgz`

## 작업 순서

### CentOS/SUSE 시스템의 작업 방법

1. 다음 명령어를 실행하여 `hosts.txt` 파일을 엽니다.
```
vi /etc/hosts
```
2. 아래 예시와 같이 **i** 또는 **Insert** 를 눌러 편집 모드로 전환한 후 [CVM IP+SSH 포트 번호+계정 +기존 비밀번호+새 비밀번호] 형식에 맞게 수정할 CVM 정보를 `hosts.txt` 파일에 추가합니다.
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 각 행의 정보는 곧 하나의 CVM을 나타냅니다. 공용 네트워크에서 해당 스크립트를 실행할 경우 CVM IP를 **공인 IP**로 입력하고, 내부 네트워크에서 해당 스크립트를 실행할 경우 CVM IP를 **개인 IP**로 입력합니다.
>
3. **Esc**를 누르고 **:wq**를 입력하면 파일을 저장 및 리턴합니다.
4. 다음 명령어를 실행하여 스크립트 파일을 실행합니다.
```
./batch-chpasswd.py
```
다음과 같은 결과를 리턴하면 재설정 성공입니다.
```
change password for root@10.0.0.1
spawn ssh root@10.0.0.1 -p 22
root password: 
Authentication successful.
Last login: Tue Nov 17 20:22:25 2015 from 10.181.XXX.XXX
[root@VM_18_18_centos ~]# echo root:root | chpasswd
[root@VM_18_18_centos ~]# exit
logout
change password for root@10.0.0.2
spawn ssh root@10.0.0.2 -p 22
root password: 
Authentication successful.
Last login: Mon Nov  9 15:19:22 2015 from 10.181.XXX.XXX
[root@VM_19_150_centos ~]# echo root:root | chpasswd
[root@VM_19_150_centos ~]# exit
logout
```

### Ubuntu 시스템의 작업 방법

1. 다음 명령어를 실행하여 `hosts.txt` 파일을 엽니다.
> 이곳에서 시스템 기본 편집기를 호출하며, 다른 파일 편집기로도 편집할 수 있습니다.
>
```
sudo gedit /etc/hosts
```
2. 아래 예시와 같이 **i** 또는 **Insert** 를 눌러 편집 모드로 전환한 후 [CVM IP+SSH 포트 번호+계정 +기존 비밀번호+새 비밀번호] 형식에 맞게 수정할 CVM 정보를 `hosts.txt` 파일에 추가합니다.
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 각 행의 정보는 곧 하나의 CVM을 나타냅니다. 공용 네트워크에서 해당 스크립트를 실행할 경우 CVM IP를 **공인 IP**로 입력하고, 내부 네트워크에서 해당 스크립트를 실행할 경우 CVM IP를 **개인 IP**로 입력합니다.
>
3. 다음 명령어를 실행하여 네트워크를 재시작합니다.
```
sudo rcnscd restart
```
4. 다음 명령어를 실행하여 스크립트 파일을 실행합니다.
```
python batch-chpasswd.py
```
