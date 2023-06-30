## 장애 현상

로컬 서버가 인스턴스를 ping하지 못합니다. 가능한 원인은 다음과 같습니다.
- 잘못된 대상 서버 설정
- 도메인 이름 확인 실패
- 연결 오류

로컬 네트워크가 정상이면(로컬 네트워크에서 다른 웹 사이트를 ping할 수 있음) 다음과 같이 문제를 해결하십시오.
- [인스턴스가 public IP 주소로 구성되었는지 확인](#isConfigurePublicIP)
- [보안 그룹 설정 확인](#CheckSecurityGroupSetting)
- [운영 체제 설정 확인](#CheckOSSetting)
- [기타 작업 수행](#OtherOperations)

## 처리 단계


### 인스턴스가 public IP 주소로 구성되었는지 확인[](id:isConfigurePublicIP)

<dx-alert infotype="explain" title="">
인스턴스는 public IP 주소가 있는 경우에만 Internet의 다른 컴퓨터에 액세스할 수 있습니다. 그렇지 않으면 사설망 IP 주소 외부를 통해 인스턴스를 ping할 수 없습니다.
</dx-alert>


1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. ‘인스턴스’ 페이지에서 다음 그림과 같이 ping할 인스턴스의 ID/이름을 선택하여 인스턴스 세부 정보 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/12dfabc6420688ebb0dd0f1a8f4d7188.png)
3. ‘네트워크 정보’에서 인스턴스가 public IP 주소로 구성되어 있는지 확인하십시오.
   - 구성되어 있는 경우, [보안 그룹 설정 확인](#CheckSecurityGroupSetting)을 진행하십시오.
   - 구성되어 있지 않은 경우, [클라우드 리소스의 EIP 바인딩](https://intl.cloud.tencent.com/document/product/213/16586)을 확인하십시오.


### 보안 그룹 설정 확인[](id:CheckSecurityGroupSetting)

보안 그룹은 연결된 인스턴스의 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽입니다. 보안 그룹 규칙에서 프로토콜, 포트 및 정책을 지정할 수 있습니다. ping 테스트는 ICMP를 사용하기 때문에 해당 인스턴스와 연결된 보안 그룹에서 해당 프로토콜이 허용되는지 확인해야 합니다. 인스턴스와 해당 인바운드 및 아웃바운드 규칙과 연결된 보안 그룹을 보려면 다음 단계를 수행하십시오.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. ‘인스턴스’ 페이지에서 보안 그룹으로 설정할 인스턴스의 ID/이름을 선택하여 다음 그림과 같이 인스턴스 세부 정보 페이지로 들어갑니다.
3. **보안 그룹** 탭을 클릭하여 다음 이미지와 같이 이 인스턴스의 보안 그룹 관리 페이지로 들어갑니다.
![](https://main.qcloudimg.com/raw/bf5881258356a0af748ae16d9cf321a2.png)
4. 인스턴스와 연결된 보안 그룹과 자세한 인바운드 및 아웃바운드 규칙을 확인하여 이 보안 그룹이 ICMP를 허용하는지 확인합니다.
   - 허용하는 경우, [운영 체제 설정 확인](#CheckOSSetting)을 진행하십시오.
   - 허용하지 않는 경우, ICMP 프로토콜 정책을 허용으로 설정하십시오.


### 운영 체제 설정 확인[](id:CheckOSSetting)

인스턴스의 운영 체제에 따라 구성을 확인할 방법을 선택합니다.
- Linux 운영 체제의 경우 [Linux 커널 매개변수 및 방화벽 설정 확인](#CheckLinux)을 진행하십시오.
- Windows 운영 체제의 경우 [Windows 방화벽 설정 확인](#CheckWindows)을 진행하십시오. 방화벽 설정이 올바르면 [Windows 네트워크 설정 재설정](#reset)을 시도하십시오.


#### Linux 커널 매개변수 및 방화벽 설정 확인[](id:CheckLinux)

<dx-alert infotype="explain" title="">
Linux 운영 체제에서 ping 테스트가 허용되는지 여부는 커널 및 방화벽 설정에 따라 다릅니다. 둘 중 하나가 ping 테스트를 거부하면 ‘Request timeout’이 발생합니다.
</dx-alert>

##### icmp_echo_ignore_all 커널 매개변수 확인

1. VNC를 통해 인스턴스에 로그인합니다. 자세한 내용은 다음을 참고하십시오.
   - [VNC를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32494)합니다.
   - [VNC를 사용하여 Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/32496)
2. 다음 명령어를 실행하여 시스템의 icmp_echo_ignore_all 설정을 확인합니다.
```
cat /proc/sys/net/ipv4/icmp_echo_ignore_all
```
   - 0이 반환되면 모든 ICMP Echo 요청이 시스템에서 허용됩니다. 이 경우 [방화벽 설정 확인](#CheckLinuxFirewall)에서 확인하십시오.
   - 1이 반환되면 모든 ICMP Echo 요청이 시스템에서 거부됩니다. 이 경우 [3단계](#Linux_step03)에서 확인하십시오.

3. [](id:Linux_step03)다음 명령을 실행하여 icmp_echo_ignore_all 커널 매개변수의 설정을 수정하십시오.
```
echo "0" >/proc/sys/net/ipv4/icmp_echo_ignore_all
```


##### 방화벽 설정 확인[](id:CheckLinuxFirewall)

다음 명령을 실행하여 방화벽 규칙과 현재 서버의 해당 ICMP 규칙이 비활성화되어 있는지 확인합니다.
```
iptables -L
```
- 다음 결과가 반환되면 ICMP 규칙이 비활성화되지 않은 것입니다.
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
- 반환 결과에 ICMP 규칙이 비활성화되었다고 표시되면 다음 명령을 실행하여 활성화합니다.
```
#Chain INPUT
iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
#Chain OUTPUT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
```


#### Windows 방화벽 설정 확인[](id:CheckWindows)

1. 인스턴스에 로그인합니다.
2. **제어판**을 열고 **Windows 방화벽**을 선택합니다.
3. ‘Windows 방화벽’ 페이지에서 **고급 설정**을 선택합니다.
4. ‘고급 보안이 포함된 Windows 방화벽’ 팝업 창에서 ICMP 인바운드 및 아웃바운드 규칙이 비활성화되어 있는지 확인합니다.
   - ICMP 인바운드 및 아웃바운드 규칙이 비활성화된 경우 활성화하십시오.

### Windows 네트워크 설정 재설정

1. VPC 네트워크가 DHCP를 지원하는지 확인합니다(DHCP는 2018년 6월 이후 생성된 VPC 네트워크에서 지원됨). DHCP를 지원하지 않는 경우 네트워크 설정의 고정 IP가 올바른지 확인하십시오.
2. DHCP를 지원하는 경우 DHCP의 사설망 IP가 맞는지 확인합니다. 올바르지 않은 경우 공식 웹 사이트에서 VNC를 통해 로그인하고 PowerShell을 관리자로 실행하십시오. `ipconfig /release` 및 `ipconfig/renew`(인스턴스를 다시 시작할 필요 없이)를 구현하여 IP를 다시 가져옵니다.
3. DHCP의 IP는 맞지만 여전히 네트워크에 연결할 수 없는 경우 시작 메뉴에서 [실행]을 클릭하고 ` ncpa.cpl `을 입력한 후 확인을 클릭합니다. 로컬 연결을 열고 ENI를 비활성화 및 활성화하십시오.
4. 문제가 지속되면 관리자로 CMD에서 다음 명령을 실행하고 인스턴스를 다시 시작하십시오.
```plantext
reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles"  /f
```

### 기타 작업[](id:OtherOperations)

상기 단계를 통해 문제가 해결되지 않을 경우 다음을 참고하십시오.
- 도메인 이름을 ping할 수 없는 경우 웹사이트 구성을 확인하십시오.
- public IP 주소를 ping할 수 없는 경우 인스턴스 및 양방향 MTR 데이터(로컬 서버에서 CVM으로, CVM에서 로컬 서버로)에 대한 정보를 첨부하고 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)하여 엔지니어에게 도움을 요청하십시오.
MTR 사용 방법에 대한 자세한 내용은 [CVM 네트워크 대기 시간 및 패킷 손실](https://intl.cloud.tencent.com/document/product/213/14638)을 참고하십시오.


