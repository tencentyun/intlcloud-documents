### VNC를 사용하여 CVM에 로그인하려면 어떻게 해야 하나요?

VNC 로그인은 Tencent Cloud가 사용자에게 제공하는 Web 브라우저를 통해 CVM에 원격으로 연결하는 방식입니다. 원격 로그인 클라이언트를 설치하지 않았거나 클라이언트 원격 로그인을 사용할 수 없는 경우, VNC로 로그인하여 CVM에 연결한 후 CVM 상태를 모니터링하고, CVM 계정을 통해 기본적인 CVM 관리 작업을 진행할 수 있습니다. 구체적인 작업 순서는 다음 문서를 참조 바랍니다.
- [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)
- [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)

### Windows 서버에 다중 사용자 원격 로그인을 설정하는 방법은 무엇인가요?

Windows 서버는 다중 사용자의 동시 원격 로그인을 지원합니다. 자세한 설정 방법은 [다중 사용자의 Windows CVM에 원격 로그인 허용 설정](https://intl.cloud.tencent.com/document/product/213/32497)을 참조 바랍니다.
설정이 적용되지 않았다면 재시작 후 다시 로그인해 주세요.

### Ubuntu 시스템에서 root 사용자로 인스턴스에 로그인하려면 어떻게 해야 하나요?

Ubuntu 시스템의 기본 사용자 이름은 ubuntu 이며, 설치 과정 중에 root 계정 및 비밀번호를 설정하도록 기본 설정되어 있습니다. 필요에 따라 설정에서 root 사용자 로그인 허용을 활성화하면 됩니다. 구체적인 작업 순서는 다음과 같습니다.
1. ubuntu 계정으로 CVM에 로그인합니다.
2. <span id="Step2"></span> 다음 명령어를 실행하여 root 비밀번호를 설정합니다.
```
sudo passwd root
```
3. root 비밀번호를 입력하고 **Enter**를 누릅니다.
4. root 비밀번호를 중복 입력하고 **Enter**를 누릅니다.
다음과 같은 정보가 출력되면 root 비밀번호가 성공적으로 설정되었음을 의미합니다.
```
passwd: password updated successfully
```
5. 다음 명령어를 실행하여 `sshd_config` 환경설정 파일을 엽니다.
```
sudo vi /etc/ssh/sshd_config 
```
6. 아래 이미지와 같이 **i** 를 눌러 편집 모드로 전환한 후 `#Authentication`에서 `PermitRootLogin` 매개변수를 `yes`로 변경합니다.
> `PermitRootLogin` 매개변수가 주석으로 표시되면 첫 행의 주석 기호(`#`)를 제거합니다.
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장한 후 돌아갑니다.
8. 다음 명령어를 실행하여 ssh 서비스를 재시작합니다.
```
sudo service ssh restart
```
9. [표준 로그인 방식으로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참조하여 다음의 정보를 사용하여 Ubuntu CVM에 로그인합니다.
 - **사용자 이름**: root
 - **로그인 비밀번호**: [2단계](#Step2)에서 설정한 비밀번호를 사용합니다.
 root 계정으로 로그인에 성공하면 아래 이미지와 같이 표시됩니다.
![](https://main.qcloudimg.com/raw/a8a6ec3e2499e08d051c9ee11fdcd85e.png)

### 인스턴스 재시작 후 연결(로그인)할 수 없는 문제는 어떻게 해결하나요?

CVM의 CPU/메모리의 과부하로 인한 문제일 수 있습니다. 아래의 문서를 참조하여 해결할 수 있습니다.
- [Linux 인스턴스: CPU 혹은 메모리 점유율이 높아 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32387)
- [Windows 인스턴스: CPU 혹은 메모리 점유율이 높아 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32405)

### CVM 인스턴스에 원격 연결 시 인스턴스 연결 시간 초과 메시지가 뜨는 경우 어떻게 하나요?
다음의 문제를 진단합니다.
- 인스턴스가 실행 중인지 확인
- 인스턴스가 위치한 보안 그룹에 해당하는 보안 규칙을 추가했는지 확인. 구체적인 작업 순서는 [보안그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조 바랍니다.
- 인스턴스가 터미널 연결(SSH) 혹은 원격 데스크톱(RDP)에 해당하는 원격 서비스를 허용했는지 확인.
- 인스턴스가 연결 포트를 개방했는지 확인. 일반적으로 터미널 연결(SSH)은 22 포트를 개방하고, 원격 데스크톱(RDP)은 3389 포트를 개방합니다.

### Linux 인스턴스에 원격 연결 시 연결 거부 메시지가 뜨는 경우 어떻게 하나요?
다음의 문제를 진단합니다.
- 인스턴스가 터미널 연결(SSH) 혹은 원격 데스크톱(RDP)에 해당하는 원격 서비스를 허용했는지 확인.
- 인스턴스가 연결 포트를 개방했는지 확인. 일반적으로 터미널 연결(SSH)은 22 포트를 개방하고, 원격 데스크톱(RDP)은 3389 포트를 개방합니다.

### Linux 인스턴스에 원격 연결 시 사용자 이름 혹은 비밀번호가 틀렸다고 메시지가 뜨는 경우 어떻게 하나요?
다음의 문제를 진단합니다.
- 사용자 이름을 정확하게 입력합니다. 일반적으로 Linux 인스턴스의 사용자 이름은 root(Ubuntu 시스템의 기본 사용자 이름은 ubuntu)입니다.
- 비밀번호를 정확하게 입력합니다. 비밀번호를 잊으셨다면 비밀번호를 재설정할 수 있습니다. 구체적인 작업 순서는 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.

### Windows 인스턴스에 원격 연결 시 사용자 이름 혹은 비밀번호가 틀렸다고 메시지가 뜨는 경우 어떻게 하나요?
다음의 문제를 진단합니다.
- 사용자 이름을 정확하게 입력합니다. 일반적으로 Windows 인스턴스의 사용자 이름은 Administrator입니다.
- 비밀번호를 정확하게 입력합니다. 비밀번호를 잊으셨다면 비밀번호를 재설정할 수 있습니다. 구체적인 작업 순서는 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
- 관리자가 아닌 사용자로 Windows 인스턴스에 로그인 시 해당 사용자는 Remote Desktop Users 그룹에 속해 있어야 합니다.

### 콘솔에서 다중 사용자가 VNC 방식을 통해 CVM에 로그인할 수 있도록 지원하나요?
지원하지 않습니다. 한 사용자가 이미 로그인한 상태에는 다른 사용자가 로그인할 수 없습니다.

### CVM의 로그인 비밀번호를 잊었을 때는 어떻게 하나요?
CVM 비밀번호를 수정할 수 있습니다. 자세한 방법은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.

### 왜 IE8.0 브라우저를 사용하면 VNC로 인스턴스에 로그인할 수 없나요?
IE10 및 그 이상 버전의 IE 브라우저를 사용해야만 VNC로 인스턴스에 로그인할 수 있으니, 최신 버전의 IE 브라우저를 다운로드하시기 바랍니다.
또한, Tencent Cloud의 콘솔은 Chrome 브라우저와 호환성이 더 좋기 때문에 Chrome 브라우저를 사용할 것을 권장합니다.

### Linux 인스턴스에 원격 로그인하는 방법은 무엇인가요?
Tencent Cloud는 [WebShell 방식을 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)하는 방법을 권장합니다. 혹은 다음의 방법으로 로그인할 수 있습니다.
- [원격 로그인 소프트웨어를 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32502)
- [SSH 로그인을 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32501)
- [VNC 로그인을 사용해 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)

### Linux 인스턴스에 연결할 수 없는 경우 어떻게 하나요?
Linux 인스턴스에 연결 혹은 로그인할 수 없을 경우 [Linux 인스턴스에 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/32500)을 참조하여 문제를 해결하시기 바랍니다.
그래도 문제가 해결되지 않을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백 바랍니다.

### Windows 인스턴스에 연결할 수 없는 경우 어떻게 하나요?
Windows 인스턴스에 연결 혹은 로그인할 수 없다면 [Windows 인스턴스에 로그인할 수 없음](https://intl.cloud.tencent.com/document/product/213/10339)을 참조하여 문제를 해결하시기 바랍니다.
그래도 문제가 해결되지 않을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1)을 통해 피드백 바랍니다.

### CVM 인스턴스에 비정상적 로그인 위치가 감지되면 어떻게 하나요?
비정상적 로그인 위치가 감지되었을 경우, 다음과 같은 해결 방법이 있습니다.
1. 비정상적 위치에서 로그인한 시간대를 확인하여 본인 혹은 다른 관리자가 로그인한 것인지 확인합니다.
2. 유효한 관리자가 로그인한 것이 아닐 경우 다음과 같이 작업합니다.
 1. 즉시 [비밀번호를 재설정](https://intl.cloud.tencent.com/document/product/213/16566)합니다.
 2. 바이러스 공격 여부를 진단합니다.
 3. 보안 그룹 기능을 통해 [특정 IP만 로그인 허용](https://intl.cloud.tencent.com/document/product/213/32369)으로 설정합니다.



