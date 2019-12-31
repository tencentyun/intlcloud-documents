## 작업 시나리오

본 문서는 비 종료 상태에서 여러 Linux 시스템 CVM에 대량DMFH 비밀번호 재설정을 실행하는 작업에 대해 안내합니다.

## 스크립트 다운로드
Tencent Cloud는 사용자를 위해 재설정할 스크립트 작업을 작성하였으며 해당 재설정한 스크립트를 CVM에 다운로드 및 압축 해제하면 편리하게 온라인에서 대량으로 재설정할 수 있습니다.
경로 가져오기: `http://batchchpasswd-10016717.file.myqcloud.com/batch-chpasswd.tgz`

## 작업 순서

### CentOS/SUSE 시스템의 작업 방법

1. 다음 명령어를 실행하여 `hosts.txt` 파일을 여십시오.
```
vi /etc/hosts
```
2. **i** 또는 **Insert** 를 눌러 편집 모드로 전환한 후 [CVM IP+SSH 포트 번호+계좌 +기존 비밀번호+새 비밀번호]형식에 따라 수정할 CVM 정보를 `hosts.txt` 파일에 추가합니다. 다음과 같이 표시됩니다.
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 각 행의 정보는 CVM 1개를 대표합니다. 공용 네트워크에서 해당 스크립트를 실행할 경우 CVM IP는 **공용 네트워크 IP**로 입력하고 개인 네트워크에서 해당 스크립트를 실행할 경우 CVM IP는 **개인 IP**로 입력하면 됩니다.
>
3. **Esc**를 누르고 **:wq**를 입력하면 파일을 저장 및 리턴합니다.
4. 다음 명령어를 실행하여 스크립트 파일을 실행하십시오.
```
./batch-chpasswd.py
```
다음과 같은 결과를 리턴하면 재설정이 성공했다는 의미입니다.
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

1. 다음 명령어를 실행하여 `hosts.txt` 파일을 여십시오.
> 시스템의 기본 편집기를 호출하면 귀하도 다른 파일 편집기를 사용하여 편집할 수 있습니다.
>
```
sudo gedit /etc/hosts
```
2. **i** 또는 **Insert** 를 눌러 편집 모드로 전환한 후 [CVM IP+SSH 포트 번호+계좌 +기존 비밀번호+새 비밀번호]형식에 따라 수정할 CVM 정보를 `hosts.txt` 파일에 추가합니다. 다음과 같이 표시됩니다.
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
> 각 행의 정보는 CVM 1개를 대표합니다. 공용 네트워크에서 해당 스크립트를 실행할 경우 CVM IP는 **공용 네트워크 IP**로 입력하고 개인 네트워크에서 해당 스크립트를 실행할 경우 CVM IP는 **개인 IP**로 입력하면 됩니다.
>
3. 다음 명령어를 실행하여 네트워크를 재시작하십시오.
```
sudo rcnscd restart
```
4. 다음 명령어를 실행하여 스크립트 파일을 실행하십시오.
```
python batch-chpasswd.py
```
