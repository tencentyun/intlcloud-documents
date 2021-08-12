## 장애 현상

다음과 같은 문제로 인해 로컬 호스트에서 인스턴스로의 ping 실패 현상이 발생할 수 있습니다.
- 대상 서버의 설정이 올바르지 않은 경우
- 도메인이 올바르게 리졸브되지 않은 경우
- 링크 장애

로컬 네트워크가 정상적으로 실행(다른 웹 사이트에 ping 성공)된다는 전제하에, 다음과 같은 작업을 통해 진단할 수 있습니다.
- [인스턴스의 공인 IP 설정 여부 검사](#isConfigurePublicIP)
- [보안 그룹 설정 검사](#CheckSecurityGroupSetting)
- [시스템 설정 검사](#CheckOSSetting)
- [기타 작업](#OtherOperations)

## 작업 순서

<span id="isConfigurePublicIP"></span>
### 인스턴스의 공인 IP 설정 여부 검사

>? 인스턴스는 공인 IP가 있어야 Internet에서 다른 컴퓨터와 서로 액세스할 수 있습니다. 공인 IP가 없을 경우, 개인 IP 외부에서는 인스턴스에 바로 연결할 수 없습니다.
>
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 아래 이미지와 같이, '인스턴스 목록' 페이지에서 ping 연결이 필요한 인스턴스의 ID/이름을 선택하여 해당 인스턴스의 상세 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. '네트워크 정보' 메뉴에서 인스턴스에 공인 IP가 설정되어 있는지 확인합니다.
 - 설정되어 있을 경우, [보안 그룹 설정 검사](#CheckSecurityGroupSetting)를 진행하시기 바랍니다.
 - 설정되어 있지 않을 경우, [EIP 바인딩](https://intl.cloud.tencent.com/document/product/213/16586)을 진행하시기 바랍니다.

<span id="CheckSecurityGroupSetting"></span>
### 보안 그룹 설정 검사

보안 그룹은 하나의 가상 방화벽으로, 연결된 인스턴스의 인바운드 트래픽과 아웃바운드 트래픽을 제어할 수 있으며, 보안 그룹의 규칙으로 프로토콜, 포트 및 정책 등을 지정할 수 있습니다. Ping은 ICMP 프로토콜을 사용하므로, 인스턴스와 연관된 보안 그룹이 ICMP를 허용하는지 확인하시기 바랍니다. 다음 작업을 실행하여, 인스턴스가 사용하는 보안 그룹 및 자세한 인바운드/아웃바운드 규칙을 조회하실 수 있습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. '인스턴스 목록' 페이지에서 보안 그룹 설정이 필요한 인스턴스의 ID/이름을 선택하여 해당 인스턴스의 상세 페이지로 진입합니다.
3. 아래 이미지와 같이, [Security Group] 탭을 선택하여 해당 인스턴스의 보안 그룹 관리 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. 인스턴스가 사용하는 보안 그룹과 상세한 인바운드/아웃바운드 규칙에 따라, 인스턴스를 연결할 보안 그룹이 ICMP를 허용하는지 확인합니다.
 - ICMP를 허용할 경우, [시스템 설정 검사](#CheckOSSetting)를 진행하시기 바랍니다.
 - ICMP를 허용하지 않을 경우, ICMP 프로토콜 정책을 허용으로 설정하시기 바랍니다.

<span id="CheckOSSetting"></span>
### 시스템 설정 검사

인스턴스의 운영 체제 유형에 맞는 검사 방식을 사용합니다.
- Linux 운영 체제의 경우 [Linux 커널 매개변수 및 방화벽 설정 검사](#CheckLinux)를 진행하시기 바랍니다.
- Windows 운영 체제의 경우 [Windows 방화벽 설정 검사](#CheckWindows)를 진행하시기 바랍니다.

<span id="CheckLinux"></span>
#### Linux 커널 매개변수 및 방화벽 설정 검사

>? Linux 시스템의 ping 허용 여부는 커널과 방화벽 설정에 의해 결정되며, 둘 중 한 항목이라도 금지되었을 경우 ping 패키지의 "Request timeout" 현상을 초래할 수 있습니다.

##### 커널 매개변수 icmp_echo_ignore_all 검사

1. 인스턴스에 로그인합니다.
2. 다음 명령어를 실행하여 시스템의 icmp_echo_ignore_all 설정을 조회합니다.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
 - 출력 결과가 0일 경우, 시스템이 모든 ICMP Echo 요청을 허용하였음을 의미하므로 [방화벽 설정 검사](#CheckLinuxFirewall)를 진행하시기 바랍니다.
 - 출력 결과가 1일 경우, 시스템이 모든 ICMP Echo 요청을 금지하였음을 의미하므로 [3단계](#Linux_step03)를 실행하시기 바랍니다.
3. <span id="Linux_step03">다음 명령어를 실행하여 커널 매개변수 icmp_echo_ignore_all의 설정을 수정합니다.</span>
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

<span id="CheckLinuxFirewall"></span>
##### 방화벽 설정 검사

다음 명령어를 실행하여 현재 서버의 방화벽 규칙 및 ICMP에 상응하는 규칙이 금지되었는지 확인합니다.
```
iptables -L
```
- 다음의 결과를 출력할 경우, ICMP에 상응하는 규칙이 금지되지 않았음을 의미하므로 [도메인의 ICP비안 여부 검사](#CheckDomainRegistration)를 진행하시기 바랍니다.
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
- ICMP에 상응하는 규칙이 금지되었다는 결과가 출력될 경우, 다음 명령어를 실행하여 해당 규칙을 활성화하시기 바랍니다.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```

<span id="CheckWindows"></span>
#### Windows 방화벽 설정 검사

1. 인스턴스에 로그인합니다.
2. [제어판]을 열고 [Windows 방화벽 설정]을 선택합니다.
3. 'Windows 방화벽' 인터페이스에서 [고급 설정]을 선택합니다.
4. 팝업된 '고급 보안 Windows 방화벽' 창에서 ICMP에 관련된 인바운드/아웃바운드 규칙이 금지되었는지 확인합니다.
 - ICMP에 관련된 인바운드/아웃바운드 규칙이 비활성화되었을 경우, 해당 규칙을 활성화하시기 바랍니다.


<span id="OtherOperations"></span>
### 기타 작업

위의 순서를 통해 문제가 해결되지 않을 경우 다음을 참조 바랍니다.
- 도메인 ping에 실패한다면, 웹 사이트 설정을 검사하시기 바랍니다.
- 공인 IP ping에 실패한다면, 인스턴스 관련 정보 및 양방향 MTR 데이터(로컬에서 CVM으로, CVM에서 로컬로)를 첨부하여, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 엔지니어에게 진단을 요청하시기 바랍니다.
MTR 사용 방법은 [서버 네트워크 딜레이 및 패킷 손실 처리](https://intl.cloud.tencent.com/document/product/213/14638)를 참조 바랍니다.
