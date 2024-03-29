## 문제 설명
로컬 컴퓨터가 CVM에 액세스하거나 CVM에서 기타 네트워크 리소스에 액세스 할 때 네트워크 랙을 발견합니다. `ping` 명령어를 사용하여 네트워크 패킷 존재 또는 비교적 긴 딜레인 시간이 있는지 확인합니다.

## 문제 분석
패킷 또는 긴 딜레이 시간 문제에는 백본 링크 정체, 링크 노드 장애, CVM 부하, 시스템 설정 문제 등 여러가지 원인이 있을 수 있습니다. CVM 자체 문제를 해결한 후 MTR을 사용하여 추가 진단을 받으실 수 있습니다.
MTR은 네트워크 진단 도구이며 해당 툴이 진단을 완료한 보고서는 사용자가 네트워크 문제의 핵심을 확인할 수 있도록 도와줍니다.

## 해결 방안


본 문서는 Linux와 Windows CVM을 예로 하며 MTR 사용 방법 및 MTR 보고서 결과에 대한 분석 진행 방법을 소개합니다.
<dx-alert infotype="explain" title="">
로컬 또는 CVM에서 Ping이 비활성화된 경우 MTR에 결과가 없습니다.
</dx-alert>

실행하는 MTR의 호스트 운영 체제에 따라 MTR 소개 및 사용법을 참고하십시오.
<dx-tabs>
::: WinMTR 소개 및 사용(Windows 운영 체제)][](id:MTRofWindows)
**WinMTR:** Windows 시스템의 무료 네트워크 진단 도구에 사용되며 Ping 과 tracert의 기능을 결합하였습니다. 그래픽 인터페이스는 시각적으로 각각의 노드의 응답 시간과 패킷 상황을 확인할 수 있게 해줍니다.

#### WinMTR 설치
1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 공식 웹 사이트 브라우저 액세스를 통해(또는 합법 경로) 대응하는 운영 체제 유형의 WinMTR 설치 패키지를 다운로드하십시오.
3. WinMTR 설치 패키지를 압축 해제하십시오.

#### WinMTR 사용
1. WinMTR.exe를 더블 클릭하여 WinMTR 툴을 여십시오.
2. WinMTR 창의  Host에서 타깃 서버 IP 또는 도메인 이름을 입력하고 **Start**를 클릭하십시오. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/7aa2d2e76b86deabd6d0248ecf89de56.png)
3. 실제 상황에 따라 WinMTR이 잠시 실행될 때까지 기다린 뒤 **Stop**을 클릭하여 테스트를 종료하십시오. 아래 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/5d73f806c0252d26755d584e874c26f1.png)
다음은 테스트 결과 주요 정보입니다.
 - **Hostname**: 타깃 서버로 통과하는 각 호스트 IP 또는 명칭.
 - **Nr**: 노드를 통과하는 수량.
 - **Loss%**: 대응하는 노드의 패킷 손실률.
 - **Sent**: 전송된 데이터 패키지 수량.
 - **Recv**: 응답 받은 수량.
 - **Best**: 가장 짧은 응답 시간.
 - **Avrg**: 평균 응답 시간.
 - **Worst**: 가장 긴 응답 시간.
 - **Last**: 가장 최근 응답 시간.


:::
::: MTR 소개 및 사용(Linux 운영 체제)][](id:MTRofLinux)
**MTR:** Linux 플랫폼에서 네트워크 상태를 진단하는 도구, Ping, traceroute, nslookup의 기능을 상속하고 일반적으로 ICMP 패키지를 사용하여 두 개의 노드를 테스트하기 전의 네트워크 연결 상태입니다.

#### MTR 설치
현재 Linux가 배포한 버전은 모두 MTR이 설치되어 있습니다. 사용자의 Linux CVM에 MTR이 설치되어 있지 않다면 다음 명령어를 통해 설치를 진행할 수 있습니다.
- CentOS 운영 체제:
```
yum install mtr
```
- Ubuntu 운영 체제:
```
sudo apt-get install mtr
```

#### MTR 관련 파라미터 설명
- **-h/--help**: 도움말 메뉴 표시
- **-v/--version**: MTR 버전 정보 표시
- **-r/--report**: 보고서 형식의 결과 출력
- **-p/--split**: **--report**와 상대적으로 매 회 추적 결과를 각각 나열
- **-c/--report-cycles**: 초당 전송되는 데이터 패키지 수량 설정, 기본값 10
- **-s/--psize**: 데이터 패키지 크기 설정
- **-n/--no-dns**: IP 주소에 대해서 도메인 이름 확인을 진행하지 않음
- **-a/--address**: 사용자가 데이터 패키지의 IP 주소 전송을 설정하고 주요 사용자의 단일 서버에 여러개의 IP 주소가 있는 환경
- **-4**: IPv4
- **-6**: IPv6

#### 사용 예시
로컬 컴퓨터의 IP가 119.28.98.39인 Virtual Machine을 예로 합니다.
다음 명령어를 실행하여 보고서 형식의 MTR의 진단 보고서를 확인하십시오.
```
mtr 119.28.98.39 --report
```
다음과 유사한 정보가 반환됩니다.
```
[root@VM_103_80_centos ~]# mtr 119.28.98.39 --report
Start: Mon Feb  5 11:33:34 2019
HOST:VM_103_80_centos            Loss%    Snt    Last    Avg    Best    Wrst    StDev
1.|-- 100.119.162.130             0.0%     10     6.5    8.4     4.6    13.7      2.9
2.|-- 100.119.170.58              0.0%     10     0.8    8.4     0.6     1.1      0.0
3.|-- 10.200.135.213              0.0%     10     0.4    8.4     0.4     2.5      0.6
4.|-- 10.200.16.173               0.0%     10     1.6    8.4     1.4     1.6      0.0
5.|-- 14.18.199.58                0.0%     10     1.0    8.4     1.0     4.1      0.9
6.|-- 14.18.199.25                0.0%     10     4.1    8.4     3.3    10.2      1.9
7.|-- 113.96.7.214                0.0%     10     5.8    8.4     3.1    10.1      2.1
8.|-- 113.96.0.106                0.0%     10     3.9    8.4     3.9    11.0      2.5
9.|-- 202.97.90.206               30.0%     10    2.4    8.4     2.4     2.5      0.0
10.|-- 202.97.94.77               0.0%     10     3.5    4.6     3.5     7.0      1.2
11.|-- 202.97.51.142              0.0%     10   164.7    8.4   161.3   165.3      1.2
12.|-- 202.97.49.106              0.0%     10   162.3    8.4   161.7   167.8      2.0
13.|-- ix-xe-10-2-6-0.tcore2.LVW 10.0%     10   168.4    8.4   161.5   168.9      2.3
14.|-- 180.87.15.25              10.0%     10   348.1    8.4   347.7   350.2      0.7
15.|-- 180.87.96.21               0.0%     10   345.0    8.4   343.4   345.0      0.3
16.|-- 180.87.96.142              0.0%     10   187.4    8.4   187.3   187.6      0.0
17.|-- ???                      100.0%     10     0.0    8.4     0.0     0.0      0.0
18.|-- 100.78.119.231             0.0%     10   187.7    8.4   187.3   194.0      2.5
19.|-- 119.28.98.39               0.0%     10   186.5    8.4   186.4   186.5      0.0
```
다음은 주요 출력 정보입니다.
- **HOST:** 노드의 IP 주소 또는 도메인 이름.
- **Loss%:** 패킷 손실률.
- **Snt:** 초당 전송된 데이터 패키지의 수량.
- **Last:** 가장 최근 응답 시간.
- **Avg:** 평균 응답 시간.
- **Best:** 가장 짧은 응답 시간.
- **Wrst:** 가장 긴 응답 시간.
- **StDev:** 표준 편차, 편차값이 클수록 각 데이터 패키지가 해당 노드에서의 응답 시간 차이가 큽니다.


:::
</dx-tabs>






### 보고서 결과 분석 및 프로세스


<dx-alert infotype="explain" title="">
네트워크 비대칭으로 인해 로컬 컴퓨터에서 Virtual Machine의 네트워크 문제를 만났을 때, 양방향의 MTR 데이터(로컬 컴퓨터가 CVM로 또는 CVM이 로컬 컴퓨터로)를 수집하길 권장합니다.
</dx-alert>


1. 보고서 결과에 따라 타깃 서버 IP의 패킷 손실 여부를 확인하십시오.
 - 패킷이 손실되지 않은 경우 네트워크가 정상임을 의미합니다.
 - 패킷이 손실된 경우 [2단계](#step02)를 실행하십시오.
2. [](id:step02)결과 보고서를 조회하고 처음 패킷 손실된 노드를 찾습니다.
 - 타깃 서버의 패킷 손실이 발생하면 대상 서버의 네트워크 구성이 잘못된 것이므로 타깃 서버의 방화벽 구성을 확인하십시오.
 - 패킷 손실이 처음 3개의 홉에서 시작된 경우 일반적으로 로컬 컴퓨터 통신사 네트워크 문제일 수 있으며 기타 웹 사이트에 액세스할 때 동일한 상황의 발생 여부를 확인하십시오. 동일한 상황이 발생할 경우 ISP에 피드백을 보내 진행하십시오.
 - 패킷 손실이 빈번하다면 실제로 네트워크가 불안정한 시나리오입니다. 상담을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 진행하시고, 엔지니어가 진단할 수 있도록 테스트 화면 캡처를 첨부하십시오.



