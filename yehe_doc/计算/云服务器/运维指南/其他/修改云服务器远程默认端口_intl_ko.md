## 작업 시나리오
시스템 기본 포트를 사용하면 리스크가 크기 때문에 소프트웨어 스캔 및 공격을 받기 쉽습니다. 포트 공격으로 인해 CVM에 원격 연결할 수 없는 상황에 대비하여 CVM 기본 원격 포트를 흔하지 않은 포트로 수정함으로써 CVM의 안전을 강화할 수 있습니다.

서비스 포트 수정은 보안 그룹 규칙과 CVM에서 동기화 수정해야, 정식으로 적용됩니다. 아래의 작업은 CVM의 기본 원격 포트를 수정하는 방법을 소개하며, CVM 운영 체제 유형에 따라 수정 방식을 선택합니다.
- [Windows CVM 기본 원격 포트 수정](#ModifyWindowsCVMPort)
- [Linux CVM 기본 원격 포트 수정](#ModifyLinuxCVMPort)

## 작업 순서

<span id="ModifyWindowsCVMPort"></span>
### Windows CVM 기본 원격 포트 수정
>아래의 작업은 Windows Server 2012 운영 체제를 예로 들며, 운영 체제 버전과 언어 차이로 인해 세부 작업 순서에 약간의 차이가 있습니다.
>
1. [VNC로 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496).
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> 클릭 후, "Windows PowerShell" 창을 엽니다.
3. "Windows PowerShell" 창에서 **regedit**를 입력한 후 **Enter**를 눌러 "레지스트리 편집기" 창을 엽니다.
4. 왼쪽의 레지스트리 바에서 [HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[Terminal Server]>[Wds]>[rdpwd]>[Tds]>[tcp] 디렉터리를 차례대로 펼칩니다.
5. <span id="Windows_step05"></span>아래 이미지와 같이 [tcp] 중의 PortNumber를 찾아 PortNumber 데이터(즉 3389 포트 번호)를 0 - 65535 사이의 미사용 포트로 수정합니다.
![](https://main.qcloudimg.com/raw/7044cef95fd7e56b56946afdb64de346.png)
6. 왼쪽의 레지스트리 바에서 [HKEY_LOCAL_MACHINE]>[SYSTEM]>[CurrentControlSet]>[Control]>[Terminal Server]>[WinStations]>[RDP-Tcp] 디렉터리를 차례대로 펼칩니다.
7. [RDP-Tcp] 에서 PortNumber를 찾아 [RDP-Tcp] 안의 PortNumber 데이터(포트 번호)를 [tcp] 안의 PortNumber 데이터(포트 번호)와 동일한 포트 번호로 수정합니다.
![](https://main.qcloudimg.com/raw/fa54eb32c20dcc8a7c942c8e707fa665.png)
8. (선택)사용자의 CVM이 방화벽을 활성화한 경우, 새로운 포트를 방화벽에 추가하고 연결 허용을 설정해야 합니다.
 1. "Windows PowerShell" 창에서 **wf.msc**를 입력한 후 **Enter**를 눌러 “고급 보안 Windows 방화벽” 창을 엽니다.
 2. 아래 이미지와 같이 "고급 보안 Windows 방화벽" 창에서 [인바운드 규칙]을 선택한 후 [규칙 생성]을 클릭합니다.
![](https://main.qcloudimg.com/raw/ac93eed862e215971073912030fdbc41.png)
 3. "새 인바운드 규칙 마법사" 창의 "규칙 종류" 단계에서 [포트]를 선택한 후 [다음]을 클릭합니다.
 4. 아래 이미지와 같이 "새 인바운드 규칙 마법사" 창의 "프로토콜 및 포트" 단계에서 [TCP]를 선택하고 [특정 로컬 포트]를 [5단계](#Windows_step05)에서 설정한 포트 번호로 작성한 후 [다음]을 클릭합니다.
 ![](https://main.qcloudimg.com/raw/73a7ca280f4f6b733d687597014b57b4.png)
 5. "새 인바운드 규칙 마법사" 창의 "작업" 단계에서 [연결 허용]을 선택한 후 [다음]을 클릭합니다.
 6. "새 인바운드 규칙 마법사" 창의 “프로파일” 단계에서 기본 설정을 유지한 후 [다음]을 클릭합니다.
 7. "새 인바운드 규칙 마법사" 창의 "이름" 단계에서 규칙 이름을 입력한 후 [완료]를 클릭합니다.
9. "Windows PowerShell" 창에서 **services.msc**를 입력한 후, **Enter**를 눌러 "서비스" 창을 엽니다.
10. "서비스" 창에서 [Remote Desktop Services]를 찾아 [Remote Desktop Services]를 우클릭한 후 [재시작]을 선택하여 원격 로그인 서비스를 재시작합니다.
11. [보안 그룹 규칙 수정](https://intl.cloud.tencent.com/document/product/213/34825)을 참조하여 프로토콜 포트가 “TCP:3389”인 보안 그룹 규칙을 [5단계](#Windows_step05)에서 설정한 포트 번호로 수정합니다.
![](https://main.qcloudimg.com/raw/a447d7e69ce95d349f0d78b5b72b9228.png)


<span id="ModifyLinuxCVMPort"></span>
### Linux CVM 기본 원격 포트 수정
>
> - Linux CVM 기본 원격 포트를 수정하기 전에, 우선 SSH 포트 번호를 추가하고 새 포트 번호로 CVM에 연결할 수 있는지 테스트한 후, 기본 22 포트를 삭제할 것을 권장합니다. 이로써 새 포트 번호로 연결할 수 없을 때 기본 22 포트를 사용하여 CVM에 연결할 수 있도록 합니다.
> - 아래의 작업은 CentOS 7.3 운영 체제를 예로 들며, 운영 체제 버전과 언어 차이로 인해 세부 작업 순서에 약간의 차이가 있습니다.
>
1. [VNC로 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494).
2. 다음 명령어를 실행하여 프로파일을 수정합니다.
```
vim /etc/ssh/sshd_config
```
3. <span id="Linux_step03"></span>아래 이미지와 같이 **i**를 눌러 편집 모드로 전환한 후, 신규 포트 콘텐츠를 추가하고 `#Port 22`아래에 새로운 `Port 신규 포트 번호`를 추가한 다음, ` Port 22`의 주석을 삭제(즉 앞에 있는 `#` 삭제)합니다.
예시: `Port 23456`.
![](https://main.qcloudimg.com/raw/54e5d9b4301271fbbeca8b2718b985dc.png)
4. **Esc**를 누르고 **:wq**를 입력하여 콘텐츠를 저장한 뒤 돌아갑니다.
5. 다음 명령어를 실행하여 구성을 수정한 후 적용합니다.
```
systemctl restart sshd.service
```
6. (선택)방화벽을 설정합니다.
 - CentOS 7 이전 버전의 Linux CVM은 기본으로 iptables 서비스를 방화벽으로 사용합니다. CVM이 iptables 규칙을 생성한 경우, 아래의 작업을 실행하여 방화벽을 설정해야 합니다:
    1. 다음 명령어를 실행하여 방화벽을 설정합니다.
```
iptables -A INPUT -p tcp --dport 신규 포트 번호 -j ACCEPT
```
예시, 신규 포트 번호가 23456이면 다음 명령어를 실행합니다.
```
iptables -A INPUT -p tcp --dport 23456 -j ACCEPT
```
    2. 다음 명령어를 실행하여 방화벽을 재시작합니다.
```
service iptables restart
```
 - CentOS 7 및 이후 버전의 Linux CVM은 기본으로 Firewalld 서비스를 방화벽으로 사용합니다. CVM이 이미 firewalld.service를 활성화한 경우, 아래의 작업을 실행하여 방화벽을 설정해야 합니다.
다음 명령어를 실행하여 [3단계](#Linux_step03)에서 새로 추가한 포트 번호의 통과를 허가합니다.
```
firewall-cmd --add-port=신규 포트 번호/tcp --permanent
```
예시, 새로 추가한 포트 번호가 23456이면 다음 명령어를 실행합니다.
```
firewall-cmd --add-port=23456/tcp --permanent
```
출력 결과가 `success`면 통과 허가 성공을 표시합니다.
7. [보안 그룹 규칙 수정](https://intl.cloud.tencent.com/document/product/213/34825)을 참조하여 프로토콜 포트가 “TCP:22”인 보안 그룹 규칙을 [3단계](#Linux_step03)에서 새로 추가한 포트 번호로 수정합니다.
![](https://main.qcloudimg.com/raw/add0bba23dc32f73b5d1fbbdad71c9ab.png)


## 인증 작업

### Windows CVM의 인증

1. 로컬 컴퓨터가 Windows 운영 체제일 때를 예로, 원격 데스크톱 연결 대화창을 엽니다.
2. 아래 이미지와 같이 [컴퓨터] 뒤쪽에 `Windows 서버의 공인 IP:수정 후의 포트 번호`를 입력한 후 [연결]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1452f968e3c2c4d4c1083bdf0742df9d.png)
3. 인터페이스에 따라 인스턴스의 관리자 계정과 비밀번호를 입력한 후 [확인]을 클릭합니다.
Windows CVM의 운영 체제 인터페이스로 이동하면 로그인 연결 성공입니다.
> 아래 이미지와 같이 RDP 파일을 사용해 Windows CVM에 로그인하는 경우, 우선 RDP 파일 중의 `full address:s` 매개변수를 수정해야 합니다.
>[](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
>

### Linux CVM의 인증

1. PuTTY 원격 로그인 소프트웨어를 예로, PuTTY 클라이언트를 엽니다.
2. 아래 이미지와 같이 PuTTY Configuration 창에서 Linux CVM의 공인 IP를 입력한 후 [Port]를 새 포트 번호로 설정하고 [Open]을 클릭합니다.
![](https://main.qcloudimg.com/raw/c89c2064ed82e738fd60fcab39b09206.png)
3. 인터페이스에 따라 Linux CVM의 사용자 이름과 비밀번호를 입력한 후 **Enter**를 누릅니다.
아래 인터페이스로 이동하면 로그인 연결 성공입니다.
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
4. 새 포트를 사용하여 Linux CVM에 성공적으로 로그인한 후 다음 명령어를 실행하여 22 기본 포트에 주석을 답니다.
```
vim /etc/ssh/sshd_config
```
5. **i**를 눌러 편집 모드로 전환한 후 `Port 22` 앞에 `#`을 입력하여 해당 포트에 주석을 답니다.
6.  **Esc**를 누르고 **:wq**를 입력하여 콘텐츠를 저장한 뒤 돌아갑니다.
7.  다음 명령어를 실행하여 설정을 수정한 후 적용합니다. 다음 로그인 시 새로운 포트를 사용하여 Linux CVM에 원격 로그인하면 됩니다.
```
systemctl restart sshd.service
```

