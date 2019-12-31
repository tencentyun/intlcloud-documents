## 장애 현상

로컬 호스트가 인스턴스를 ping 체크를 하지 않을 경우 다음과 같은 문제로 인해 발생될 수 있습니다.
- 타깃 서버의 설정이 정확하지 않습니다.
- 도메인 이름이 정확하게 확인되지 않습니다.
- 링크 장애

로컬 네트워크를 정상적 실행된다는 전제 하에 (정상적으로 다른 네트워크를 ping 보낼 수 있음) 다음과 같은 작업에 따라 조사할 수 있습니다:
- [인스턴스의 공용 네트워크 IP 구성 검사](#isConfigurePublicIP)
- [보안 그룹 설정 검사](#CheckSecurityGroupSetting)
- [시스템 설정 검사](#CheckOSSetting)
- [도메인 이름 ICP비안 검사](#CheckDomainRegistration)
- [도메인 이름 확인 검사](#CheckDNS)
- [다른 작업](#OtherOperations)

## 처리 순서

<span id="isConfigurePublicIP"></span>
### 인스턴스 공용 네트워크 IP 구성 여부 검사

> 인스턴스는 공용 네트워크 IP가 있어야 Internet에서 서로 액세스할 수 있습니다. 공용 네트워크 IP가 없을 경우 개인 IP 외부에서 인스턴스를 직접 ping이 도달할 수 없습니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오.
2. "인스턴스 목록" 페이지에서 ping 도달이 필요한 인스턴스 ID/인스턴스 이름을 선택하고 해당 인스턴스의 상세 페이지로 진입합니다. 아래 이미지를 참조하십시오.
3. "네트워크 정보"에서 인스턴스가 공용 네트워크 IP를 구성하였는지 조회합니다.
 - 예, [보안 그룹 설정 조회](#CheckSecurityGroupSetting)을 조회하십시오.
 - 아니오, [EIP 바인딩](https://intl.cloud.tencent.com/document/product/213/16586)을 조회하십시오.

<span id="CheckSecurityGroupSetting"></span>
### 보안 그룹 설정 검사

보안 그룹은 하나의 버츄얼 방화벽으로 연결된 인스턴스의 인바운드 트래픽 및 아웃바운드 트래픽을 제어할 수 있습니다. 보안 그룹의 규칙은 프로토콜, 포트 및 정책 등을 지정할 수 있습니다. ping은 ICMP 프로토콜을 사용하므로 인스턴스와 연관된 보안 그룹이 ICMP를 허용하는지 확인하십시오. 다음 작업을 실행하여 인스턴스가 사용하는 보안 그룹 및 자세한 인바운드/아웃바운드 규칙을 조회하십시오.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인하십시오.
2. "인스턴스 목록"페이지에서 보안 그룹에 대한 설정이 필요한 인스턴스 ID/인스턴스 이름을 선택하고 해당 인스턴스의 상세 페이지로 진입합니다.
3. [보안 그룹]페이지 탭을 선택하여 해당 인스턴스의 보안 그룹 관리 페이지로 진입합니다. 아래 이미지를 참조하십시오.
4. 인스턴스가 사용하는 보안 그룹 및 자세한 인바운드/아웃바운드 규칙의 조회에 따라 ICMP 허용 여부를 판단합니다.
 - 예, [시스템 설정 조회](#CheckOSSetting)하십시오.
 - 아니오, ICMP 프로토콜 정책을 허용으로 설정하십시오.

<span id="CheckOSSetting"></span>
### 시스템 설정 검사

인스턴스의 운영 체제 유형을 판단하고 다양한 검사 방식을 선택합니다.
- Linux 운영 체제의 경우 [Linux 커널 파라미터 및 방화벽 설치 검사](#CheckLinux)를 참조하십시오.
- Windows 운영 체제의 경우 [Windows 방화벽 설치](#CheckWindows) 를 참조하십시오.

<span id="CheckLinux"></span>
#### Linux 커널 파라미터 및 방화벽 설정 검사

> Linux 시스템의 ping 허용 여부는 커널과 방화벽 설정 두 가지로 결정되며 어떤 금지라도 모두 ping 패키지 "Request timeout"가 생성됩니다.

##### 커널 파라미터 icmp_echo_ignore_all 검사

1. 인스턴스에 로그인합니다.
2. 다음 명령어를 실행하여 icmp_echo_ignore_all 시스템 설정을 조회합니다.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - 리턴 결과가 0이고 시스템이 모든 ICMP Echo 요청을 허용하였음을 표시할 경우 [방화벽 설정 검사](#CheckLinuxFirewall)에서 확인하십시오.
 - 리턴 결과가 1이고 시스템이 모든 ICMP Echo 요청을 금지하였음을 표시할 경우 [3단계](#Linux_step03)에서 확인하십시오.
3. <span id="Linux_step03">다음 명령어를 실행하여 커널 파라미터 icmp_echo_ignore_all의 설정을 수정합니다.</span>
```
echo "1" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### 방화벽 설정 검사

다음 명령어를 실행하여 현재 서버의 방화벽 규칙 및 ICMP 상응하는 규칙이 금지되었는지 조회합니다.
```
iptables -L
```
- 다음 결과와 같이 리턴할 경우 ICMP 상응하는 규칙이 금지되지 않았음을 표시합니다. [도메인 이름 ICP비안 여부 검사](#CheckDomainRegistration)에서 확인하십시오.
```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         
Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination  
ACCEPT     icmp --  anywhere             anywhere             icmp echo-request
```
- 리턴 결과가 ICMP 상응하는 규칙을 금지하였을 경우 다음 명령어를 실행하여 해당 규칙을 시작하십시오.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Windows 방화벽 설정 검사

1. 인스턴스에 로그인합니다.
2. [제어판]을 열고 [Windows 방화벽 설정]을 선택합니다. 아래 이미지를 참조하십시오.
3. "Windows 방화벽" 인터페이스에서 [고급 설정]을 선택합니다. 아래 이미지를 참조하십시오.
4. 팝업된 "고급 보안 Windows 방화벽" 창에서 ICMP와 연관된 인바운드/아웃바운드 규칙이 금지되었는지 조회합니다.
 - 아래 그림과 같이 ICMP와 연관된 인바운드/아웃바운드 규칙이 금지되었을 경우 해당 규칙을 시작하십시오.
 - ICMP와 연관된 인바운드/아웃바운드 규칙이 시작되었을 경우 [도메인 이름 ICP비안 여부 검사](#CheckDomainRegistration)에서 확인하십시오.

<span id="CheckDomainRegistration"></span>
### 도메인 이름 ICP비안 여부 검사

> 공용 네트워크 IP에 ping을 보내고 도메인에 ping이 보내지지 않은 경우 도메인에 ICP비안이 없거나 도메인 이름 확인에 문제가 있는 것일 수 있습니다.
>
국가 공업정보화부는 허가를 받지 않았거나 ICP비안 절차를 밟지 않은 네트워크에 대해 인터넷 정보 서비스를 제공할 경우 위법 행위로 간주합니다. 네트워크의 정상적인 실행을 위해 먼저 ICP비안을 발급받고 네트워크를 구축하는 것을 권장합니다. ICP비안을 성공적으로 발급받은 뒤 통신관리국에서 발급한 ICP비안 번호를 제출해야만 액세스를 활성화할 수 있습니다.
- 도메인 이름에 ICP비안이 없는 경우 [도메인 이름 ICP비안](https://console.cloud.tencent.com/beian)을 실행하십시오.
- Tecent Cloud의 도메인 이름 서비스를 사용할 경우 [도메인 이름 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인하여 해당하는 도메인 이름 상황을 조회할 수 있습니다.
- 도메인 이름에 ICP비안이 있는 경우 [도메인 이름 확인 검사](#CheckDNS)에서 확인하십시오.

<span id="CheckDNS"></span>
### 도메인 이름 확인 검사

도메인에 ping 체크가 진행되지 않는 다른 원인은 도메인 이름 확인이 정확하게 구성되지 않았기 때문입니다. 사용자가 Tecent Cloud의 도메인 이름 서비스를 사용할 경우 다음 작업을 실행하여 도메인 이름 확인을 검사할 수 있습니다.
1. [도메인 이름 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
2. "나의 도메인 이름" 관리 페이지에서 도메인 이름 확인 검사가 필요한 도메인 이름 행을 선택하고[확인]을 클릭하여 도메인 이름 확인에 대한 자세한 내용을 조회합니다. 아래 이미지를 참조하십시오.

<span id="OtherOperations"></span>
### 다른 작업

위의 순서를 통해 문제가 해결되지 않을 경우 다음을 참조하십시오.
- 도메인 이름이 ping 체크가 되지 않을 경우 사용자의 네트워크 구성을 검사하십시오.
- 공용 네트워크 IP가 ping 체크가 되지 않을 경우 인스턴스의 해당 정보 및 쌍방향 MTR 데이터(로컬에서 CVM 및 CVM에서 로컬)를 첨부하여 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하고 엔지니어에게 연락하고 문제가 발생된 지점을 설명하십시오.
MTR에 대한 사용 방법은 [서버 네트워크 딜레이 및 패킷 처리](https://intl.cloud.tencent.com/document/product/213/14638)를 참조하십시오.
