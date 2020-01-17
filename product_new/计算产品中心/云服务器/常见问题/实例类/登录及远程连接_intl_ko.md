### 초기 비밀번호를 어떻게 설정합니까?

CVM을 구매할 때 사용자가 선택한 구성 방식에 따라 초기 비밀번호 설정이 달라집니다.
- 사용자가[[**빠른 구성**](https://buy.cloud.tencent.com/cvm?tab=lite)] 방식을 통해 CVM을 구매하면 CVM의 초기 비밀번호는 이메일 및 콘솔 [내부 메시지](https://console.cloud.tencent.com/message)를 통해 전송됩니다.
- 사용자가 [[**사용자 정의 구성**](https://buy.cloud.tencent.com/cvm?tab=custom)]을 통해 CVM을 구매하면 로그인 방식에 따른 초기 비밀번호 설정 방법은 다음과 같습니다.
<table>
	<tr><th>로그인 방식</th><th>설명</th></tr>
	<tr><td>비밀번호 자동 생성</td><td>초기 비밀번호는 이메일과 콘솔<a href="https://console.cloud.tencent.com/message">내부 메시지</a>를 통해 전송됩니다.</td></tr>
	<tr><td>즉시 키 연결</td><td><b>종료</b>사용자 이름 비밀번호 로그인의 초기 비밀번호는 여전히 이메일 및 콘솔<a href="https://console.cloud.tencent.com/message">내부 메시지</a>를 통해 전송됩니다.</td></tr>
	<tr><td>비밀번호 설정</td><td>사용자 정의 비밀번호는 초기 비밀번호입니다.</td></tr>
</table>

자세한 내용은 [비밀번호 로그인 관리](https://intl.cloud.tencent.com/document/product/213/17008)를 참조하십시오.

### 비밀번호를 어떻게 재설정 합니까?

[인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)에서 재설정하십시오.

### 비밀번호 재설정이 실패하면 어떻게 해야 합니까?

사용자가 재설정할 인스턴스가 종료되었는지 확인하십시오.
- 종료되지 않은 경우 [인스턴스 종료](https://intl.cloud.tencent.com/document/product/213/4929)한 후 다시 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 진행하십시오.
- 사용자의 인스턴스가 종료된 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 엔지니어에게 문의하고 문제를 해결하십시오.

### Linux 인스턴스에 SSH 키 연결 후，사용자 이름 비밀번호를 사용하여 로그인할 수 없는 이유는 무엇입니까?

CVM에 SSH 키 연결 후，**종료** 사용자 이름 비밀번호 로그인은 [SSH 키로 CVM 로그인](https://intl.cloud.tencent.com/document/product/213/32501)을 실행하십시오. 

### VNC을 사용하여 CVM에 로그인하려면 어떻게 해야 합니까?

VNC 로그인은 Tencent Cloud가 사용자에게 제공하는 Web 브라우저를 통해 CVM에 원격으로 연결하는 방식입니다. 클라이언트 원격 로그인을 설치하지 않았거나 클라이언트 원격 로그인을 사용할 수 없는 경우 사용자는 VNC 로그인을 통해 CVM에 연결하여 CVM 상태를 모니터링하고 CVM 계정을 통해 기본적인 CVM 관리 작업을 실행할 수 있습니다. 구체적인 작업 절차는 다음 문서를 참조하십시오.
- [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)
- [VNC로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)

### Windows 서버에 여러 사용자 원격 로그인을 구성하려면 어떻게 해야 합니까?

Windows 서버는 여러 사용자 원격 로그인을 지원합니다. 구체적인 구성 방법은 [Windows CVM에 여러 사용자 원격 로그인 허용 설정](https://intl.cloud.tencent.com/document/product/213/32497)을 참조하십시오.
설정이 적용되지 않으면 재시작한 후 다시 로그인하십시오.

### Ubuntu 시스템은 어떻게 root를 사용하여 사용자 인스턴스에 로그인할 수 있습니까?

Ubuntu 시스템의 기본 사용자 이름은 ubuntu 이며 설치 과정 중에 root 계정 및 비밀번호는 설정하지 않습니다. 필요할 경우 설정에서 root 사용자 로그인 허용을 활성화합니다. 구체적인 작업 절차는 다음과 같습니다：
1. ubuntu 계정으로 CVM에 로그인합니다.
2. 다음 명령어를 실행하여 root 비밀번호를 설정합니다.
```
sudo passwd root
```
3. root 비밀번호를 입력하고 **Enter**를 누릅니다.
4. 다시 root 비밀번호를 입력하고 **Enter**를 누릅니다.
다음 정보로 리턴하면 root 비밀번호가 성공적으로 설정되었음을 나타냅니다.
```
passwd: password updated successfully
```
5. 다음 명령어를 실행하여 `sshd_config` 구성 파일을 여십시오.
```
sudo vi /etc/ssh/sshd_config 
```
6. **i** 를 눌러 편집 모드로 전환한 후 `#Authentication`에서 `PermitRootLogin` 파라미터를 `yes`로 수정합니다. 아래 이미지를 참조하십시오.
> `PermitRootLogin` 파라미터가 주석으로 표시되면 첫 행의 주석 기호(`#`)를 제거하십시오.
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 리턴합니다.
8. 다음 명령어를 실행하여 ssh 서비스를 재시작합니다.
```
sudo service ssh restart
```
9. root 계정 비밀번호로 Ubuntu CVM에 로그인합니다.

### 실행 중인 Linux 인스턴스 비밀번호를 어떻게 대량으로 재설정할 수 있습니까?

종료하지 않은 상황에서 대량으로 Linux 인스턴스 비밀번호 재설정 작업을 실행할 경우 [클릭하여 다운로드](http://batchchpasswd-10016717.file.myqcloud.com/batch-chpasswd.tgz?_ga=1.165307193.726382295.1500898081)하고 대량으로 스크립트를 재설정 및 실행할 수 있습니다. 스크립트를 대량으로 재설정하는 방법은 다음과 같습니다.
> 
> - 사용자가 공용 네트워크 기기에서 해당 스크립트를 실행할 경우 hosts.txt 파일의 IP에 인스턴스의 공용 네트워크 IP를 입력합니다.
> - 사용자가 내부 네트워크 기기에서 해당 스크립트를 실행할 경우 인스턴스의 개인 IP를 입력할 수 있습니다.
> 
1. 작업할 인스턴스의 IP，SSH 포트，계정，오래된 비밀번호와 새 비밀번호를 hosts.txt 파일에 입력하고 각 행은 1개 호스트를 대표합니다. 예를 들면 다음과 같습니다.
```
10.0.0.1 22 root old_passwd new_passwd 
10.0.0.2 22 root old_passwd new_passwd
```
2. 다음 코드를 실행하십시오.
```
./batch-chpasswd.py
```
리턴 예시
```
change password for root@10.0.0.1
spawn ssh root@10.0.0.1 -p 22
root's password: 
Authentication successful.
Last login: Tue Nov 17 20:22:25 2017 from 10.181.225.39
[root@VM_18_18_centos ~]# echo root:root | chpasswd
[root@VM_18_18_centos ~]# exit
logout
```
```
change password for root@10.0.0.2
spawn ssh root@10.0.0.2 -p 22
root's password: 
Authentication successful.
Last login: Mon Nov  9 15:19:22 2017 from 10.181.225.39
[root@VM_19_150_centos ~]# echo root:root | chpasswd
[root@VM_19_150_centos ~]# exit
logout
```
