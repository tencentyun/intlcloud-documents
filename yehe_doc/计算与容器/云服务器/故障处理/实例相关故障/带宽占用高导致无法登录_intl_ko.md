
본 문서는 대역폭의 높은 점유율로 인해 Linux와 Windows CVM이 원격 연결할 수 없는 문제에 대한 해결 및 솔루션을 소개합니다.

## 장애 현상
- [Tencent Cloud CVM 콘솔](https://console.cloud.tencent.com/cvm/index) 로그인을 통해 CVM의 대역폭 모니터링 데이터에 대역폭 점유율 높음으로 표시되어 Tencent Cloud CVM에 연결할 수 없음을 확인했습니다.
<!--  -[자가 진단](https://console.cloud.tencent.com/workorder/check) 툴을 통해 대역폭 점유율이 높은 문제를 진단합니다. -->

## 장애 진단 및 처리

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 점검 예정인 CVM을 선택하여 [Log In]을 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3. 팝업된 "Windows/Linux 인스턴스 로그인" 창에서 [Alternative login methods(VNC)]]을 선택하고 [Log In Now]을 클릭하여 CVM에 로그인합니다.
4. 팝업된 로그인 창 왼쪽 상단의 "원격 명령어 발송"을 선택하고 **Ctrl-Alt-Delete**를 클릭하여 시스템 로그인 인터페이스에 접속합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Windows 서버 관련
VNC 방식으로 Windows CVM에 로그인한 후 사용자는 다음 작업을 실행해야 합니다.
>? 다음 작업은 Windows Server 2012 시스템의 CVM을 예로 듭니다.
>
1. CVM에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>을 클릭하고 [작업 관리자]를 선택하여 "작업 관리자" 창을 엽니다.
2. [성능] 탭을 선택하고 [리소스 모니터 열기]를 클릭합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/a635da7e769cc1424b225674803e5cb1.png)
3. 열린 "리소스 모니터"에서 대역폭 소모가 많은 프로세스를 조회하고, 사용자의 실제 비즈니스에 근거해 해당 프로세스가 정상인지 판단합니다. 아래 이미지 참조
![](https://main.qcloudimg.com/raw/6a131472fc52bb4f5c4d5f57a1b7b010.png)
 - 대역폭 소모가 많은 프로세스가 비즈니스 프로세스일 경우, 액세스량 변화로 인한 것인 지, 최적화 용량 또는 [서버 구성 업그레이드](https://intl.cloud.tencent.com/document/product/213/2178)가 필요한지 여부를 분석해야 합니다.
 - 대역폭 소모가 많은 프로세스가 비정상 프로세스일 경우, 트로이 목마와 같은 바이러스로 인한 것일 수 있으므로 자체로 프로세스를 종료하거나 보안 툴을 사용해 바이러스를 제거할 수 있으며, 데이터를 백업한 후 시스템을 재설치할 수도 있습니다.
 >! Windows 시스템에서 많은 바이러스 프로그램이 시스템 프로세스처럼 위장하기 때문에 [작업 관리자]>[프로세스] 중의 프로세스 정보를 통해 일차적으로 감별할 수 있습니다.
 > 정상적인 시스템 프로세스는 모두 완전한 서명과 설명이 있으며, 대부분 C:\Windows\System32 디렉터리에 있습니다. 바이러스 프로그램의 이름이 시스템 프로세스와 같을 수 있으나 서명과 설명이 부족하고, 이상한 위치에 있을 수 있습니다.
 > 
 - 대역폭 소모가 많은 프로세스가 Tencent Cloud 모듈 프로세스인 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 당사에 연락하여 진단하시기 바랍니다.

### Linux 서버 관련
VNC 방식으로 Linux CVM에 로그인한 후 다음 작업을 실행해야 합니다.
>? 다음 작업은 CentOS 7.6 시스템의 CVM을 예로 듭니다.
>
1. 다음 명령어를 실행하여 iftop 툴(iftop 툴은 Linux 서버의 트래픽 모니터링 미니 툴임)을 설치합니다.
```
yum install iftop -y
```
>? Ubuntu 시스템인 경우,  `apt-get install iftop -y` 명령어를 실행하세요.
>
2. 다음 명령어를 실행하여 lsof를 설치합니다.
```
yum install lsof -y
```
3. 다음 명령어를 실행하여 iftop를 실행합니다. 아래 이미지 참조
```
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`, `=>` 는 트래픽의 방향 표시
 - TX는 트래픽 발송 표시
 - RX는 트래픽 수신 표시
 - TOTAL은 전체 트래픽 표시
 - Cum는 현재 시간까지 iftop을 실행한 전체 트래픽 표시
 - peak는 트래픽 피크 표시
 - rates는 각각 지난 2s, 10s 및 40s의 평균 트래픽 표시
4. iftop 중 트래픽을 소모하는 IP에 따라 다음 명령어를 실행하고, 해당 IP에 연결된 프로세스를 조회합니다.
```
lsof -i | grep IP
```
예시, 트래픽을 소모한 IP가 201.205.141.123인 경우, 다음 명령어를 실행합니다.
```
lsof -i | grep 201.205.141.123
```
출력한 아래의 결과에 따라 해당 서버의 대역폭이 주로 SSH 프로세스에 의해 소모된다는 것을 알 수 있습니다.
```
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. 대역폭을 소모하는 프로세스를 조회하여 해당 프로세스가 정상인지 판단합니다.
 - 대역폭 소모가 많은 프로세스가 비즈니스 프로세스일 경우, 액세스량 변화로 인한 것인 지, 최적화 용량 또는 [서버 구성 업그레이드](https://intl.cloud.tencent.com/document/product/213/2178)가 필요한지 여부를 분석해야 합니다.
 - 대역폭 소모가 많은 프로세스가 비정상 프로세스일 경우, 트로이 목마와 같은 바이러스로 인한 것일 수 있으므로 자체로 프로세스를 종료하거나 보안 툴을 사용해 바이러스를 제거할 수 있으며, 데이터를 백업한 후 시스템을 재설치할 수도 있습니다.
 - 대역폭 소모가 많은 프로세스가 Tencent Cloud 모듈 프로세스인 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 당사에 연락하여 진단하시기 바랍니다.


타깃 IP 지역을 확인하시길 권장하며, [What is my IP address](https://whatismyipaddress.com/)를 통해 IP 지역을 조회할 수 있습니다. 타깃 IP 지역이 해외로 표시된 경우 보안 취약점이 더 클 수 있으니 중점적으로 유의하시기 바랍니다!

