본 문서는 고대역폭 사용으로 인한 Linux 또는 Windows CVM 로그인 문제를 진단하고 해결하는 방법을 설명합니다.

## 장애 현상
- [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에서 CVM의 대역폭 모니터링 데이터는 대역폭 사용량이 너무 높고 CVM에 대한 연결이 실패함을 보여줍니다.
- [자가 진단](https://console.cloud.tencent.com/workorder/check) 툴을 통한 대역폭 사용량이 너무 높습니다.

## 장애 진단 및 처리

1. VNC를 사용하여 실제 클라우드 서버 인스턴스에 로그인합니다.
 - Windows 인스턴스: [VNC를 사용하여 Windows 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32496)
 - Linux 인스턴스: [VNC를 사용하여 Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/32494)
2. 클라우드 서버 문제 해결:
<dx-tabs>
::: Windows CVM
VNC를 사용하여 Windows CVM에 로그인한 후 다음 작업을 수행합니다.
<dx-alert infotype="explain" title="">
다음 작업은 Windows Server 2012 시스템이 있는 CVM을 예로 들어 설명합니다.
</dx-alert>

1. CVM에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;"></img>을(를) 클릭합니다. **작업 관리자**를 선택하여 **작업 관리자** 창을 엽니다.
4. **성능** 탭 페이지를 선택하고 **리소스 모니터 열기**를 클릭합니다. 
5. **리소스 모니터**가 열리면 어떤 프로세스가 더 많은 대역폭을 사용하는지 확인합니다. 실제 비즈니스에 따라 프로세스가 정상적인지 확인합니다. 
 - 대역폭을 많이 소모하는 프로세스가 정상이라면 접속량의 변화 때문인지, 용량 최적화나 [CVM 구성 업그레이드](https://intl.cloud.tencent.com/document/product/213/2178)가 필요한지 확인합니다.
 - 대역폭을 많이 소모하는 프로세스가 비정상적인 경우 바이러스나 트로이 목마가 있을 수 있습니다. 프로세스를 직접 종료하거나 보안 소프트웨어를 사용할 수 있습니다. 데이터 백업 후 시스템을 다시 설치할 수도 있습니다.
<dx-alert infotype="notice" title="">
Windows 시스템에서 많은 바이러스 프로세스가 시스템 프로세스로 위장합니다. **작업 관리자** > **프로세스**에서 프로세스 정보를 사용하여 예비 검사를 수행할 수 있습니다.
일반 시스템 프로세스에는 완전한 서명과 설명이 있으며 대부분은 C:\Windows\System32 디렉터리에 있습니다. 바이러스 프로그램은 시스템 프로세스와 이름이 같을 수 있지만 서명이나 설명이 없습니다. 위치도 비정상적일 것입니다.
</dx-alert>
 - 대역폭을 많이 사용하는 프로세스가 Tencent Cloud 구성 요소 프로세스인 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 문의하십시오. 문제를 찾고 해결하는 데 도움을 드리겠습니다.
:::
::: Linux CVM
VNC를 사용하여 Linux CVM에 로그인한 후 다음 작업을 수행합니다.
<dx-alert infotype="explain" title="">
다음 작업은 CentOS 7.6 시스템이 있는 CVM을 예로 들어 설명합니다.
</dx-alert>


1. 다음 명령을 실행하여 iftop 툴을 설치합니다. iftop 툴은 Linux CVM용 트래픽 모니터링 가젯입니다.
```shellsession
yum install iftop -y
```
<dx-alert infotype="explain" title="">
Ubuntu 시스템의 경우 `apt-get install iftop -y` 명령을 실행합니다.
</dx-alert>
2. 다음 명령을 실행하여 lsof를 설치합니다.
```shellsession
yum install lsof -y
```
3. 다음 명령을 실행하여 iftop을 실행합니다. 다음 이미지와 같습니다.
```shellsession
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`, `=>`는 트래픽 방향 표시
 - TX는 발송 트래픽 표시
 - RX는 수신 트래픽 표시
 - TOTAL은 총 트래픽 표시
 - Cum은 iftop이 실행되기 시작한 순간부터 지금까지의 총 트래픽 표시
 - peak는 트래픽 피크 표시
 -  rates는 각각 지난 2초, 10초 및 40초 동안의 평균 트래픽 표시
4. iftop에서 소비된 트래픽의 IP에 따라 다음 명령어를 실행하여 이 IP에 연결된 프로세스를 확인합니다.
```shellsession
lsof -i | grep IP
```
예를 들어 소비된 트래픽의 IP가 201.205.141.123인 경우 다음 명령을 실행합니다.
```shellsession
lsof -i | grep 201.205.141.123
```
다음 결과가 반환되면 SSH 프로세스에서 CVM 대역폭을 주로 사용하는 것입니다.
```shellsession
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. 대역폭을 사용하는 프로세스를 조회하고 프로세스가 정상인지 확인합니다.
 - 대역폭을 많이 소모하는 프로세스가 정상이라면 접속량의 변화 때문인지, 용량 최적화나 [CVM 구성 업그레이드](https://intl.cloud.tencent.com/document/product/213/2178)가 필요한지 확인합니다.
 - 대역폭을 많이 소모하는 프로세스가 비정상인 경우 바이러스나 트로이 목마가 있을 수 있습니다. 프로세스를 직접 종료하거나 보안 소프트웨어를 사용할 수 있습니다. 데이터 백업 후 시스템을 다시 설치할 수도 있습니다.
 - 대역폭을 많이 사용하는 프로세스가 Tencent Cloud 구성 요소 프로세스인 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 문의하십시오. 문제를 찾고 해결하는 데 도움을 드리겠습니다.


[IP138 쿼리 웹 사이트](http://www.ip138.com/)에서 목적지 IP의 위치를 확인하는 것이 좋습니다. IP 위치가 다른 국가/지역에 있는 경우 보안 위험이 더 크니 주의하십시오!

:::
</dx-tabs>





