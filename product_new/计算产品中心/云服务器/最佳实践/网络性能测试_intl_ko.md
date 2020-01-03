## 네트워크 성능 테스트 지표
<table>
<tr><th style="width: 25%;">지표</th><th>설명</th></tr>
<tr><td><b>대역폭(Mbits/초)</b></td><td>단위 시간 내(1s) 전달 가능한 빅 데이터 값(bit)</td></tr>
<tr><td><b>TCP-RR(회/초)</b></td><td>동일한 TCP의 장시간 연결 중 여러 번 Request/Response 통신을 진행할 때의 응답 효율을 표시합니다. 데이터베이스 액세스 연결에서 TCP-RR은 비교적 보편적입니다.</td></tr>
<tr><td><b>UDP-STREAM(팩/초)</b></td><td>UDP 배치 데이터 전송을 진행할 때의 데이터 전송 처리량을 표시하고 ENI의 최대 전달 능력을 반영합니다.</td></tr>
<tr><td><b>TCP-STREAM(Mbits/초)</b></td><td>TCP 배치 데이터 전송을 진행할 때의 데이터 전송 처리량을 표시합니다.</td></tr>
</table>

## 툴 기본 정보
| 지표         | 설명    |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM   | Netperf |
| 대역폭         | iperf  |
| pps 조회      | sar     |
| ENI 배열 조회 | ethtool |

## 테스트 환경 구축

### 테스트 서버 준비

- 미러 이미지: CentOS 7.4 64 비트
- 규격: S3.2XLARGE16
- 수량: 1

테스트 서버 IP 주소가 10.0.0.1라고 가정하십시오.

### 보조 트레이닝 서버 준비

* 미러 이미지: CentOS 7.4 64 비트
* 규격: S3.2XLARGE16
* 수량: 8

보조 트레이닝 서버 IP 주소를 10.0.0.2에서 10.0.0.9라고 가정하십시오.

### 테스트 툴 배포

> 테스트 환경에서 구축과 테스트할 때, 자신에게 root 사용자 권한이 있다는 것을 보장해야 합니다.
>
1. 다음 명령어를 실행하여 컴파일 환경과 시스템 상태 탐지 도구를 설치하십시오.
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. 다음 명령어를 실행하여 Netperf 압축 팩을 다운로드하십시오.
Github에서 최신 버전 [Netperf](https://github.com/HewlettPackard/netperf)을 다운받을 수 있습니다.
```
wget -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. 다음 명령어를 실행하여 Netperf 압축 팩을 해제하십시오.
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. 다음 명령어를 실행하여 Netperf에 컴파일 및 설치를 진행하십시오.
```
./configure && make && make install
```
3. 다음 명령어를 실행하여 설치가 완료되었는지 확인하십시오.
```
netperf -h
netserver -h
```
사용 도움말이 표시되면 설치가 성공적으로 완료되었음을 의미합니다.
4. 운영 체제 유형에 따라 다음 명령어를 실행하여 iperf를 설치하십시오.
```
yum install iperf	         #centos，root 권한 보장 필요
apt-get install iperf 		#ubuntu/debian， root 권한 보장 필요
```
5. 다음 명령어를 실행하여 설치가 완료되었는지 확인하십시오.
```
iperf -h
```
사용 도움말이 표시되면 설치가 성공적으로 완료되었음을 의미합니다.

## 대역폭 테스트

성능에 대한 테스트 결과가 편차를 보이지 않게 동일한 구성의 CVM 2대를 사용하여 테스트를 진행하는 것을 권장합니다. 그 중 한 대의 CVM은 테스트 서버로, 다른 한 대의 CVM는 보조 트레이닝 서버 사용됩니다. 본 예시에서는 10.0.0.1 및 10.0.0.2를 지정하여 테스트를 진행합니다.

#### 테스트 서버
다음 명령어를 실행하십시오.
```
iperf -s
```

### 보조 트레이닝 서버

다음 명령어를 실행하십시오.
```
  iperf -c ${서버 IP 주소} -b 2048M -t 300 -P ${ENI 배열 숫자}
```
예를 들어 보조 트레이닝 서버 IP 주소가 10.0.0.1이고, ENI 배열 숫자가 8일 경우 다음 명령어를 실행하십시오.
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

## UDP-STREAM 테스트

1대의 테스트 서버와 8대의 보조 트레이닝 서버를 사용하여 진행하기를 권장합니다. 이 중 10.0.0.1은 테스트 서버이고, 10.0.0.2~10.0.0.9는 보조 트레이닝 서버입니다.

#### 테스트 서버
다음 명령어를 실행하여 네트워크 pps 값을 조회하십시오.
```
netserver
sar -n DEV 2
```

### 보조 트레이닝 서버

다음 명령어를 실행하십시오.
```
./netperf -H <테스트 서버 개인 IP 주소-l 300 -t UDP_STREAM -- -m 1 &
```
보조 트레이닝 서버는 이론적으로 소량의 netperf 인스턴스를 시작하여(경험상 1대만으로도 시작할 수 있지만, 시스템 성능이 불안정한 경우에는 netperf 소량 추가하여 시작함) UDP_STREAM 한계치에 도달할 수 있습니다.
예를 들어 테스트 서버의 개인 IP 주소가 10.0.0.1일 경우에는 다음 명령어를 실행하십시오.
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

## TCP-RR 테스트

1대의 테스트 서버와 8대의 보조 트레이닝 서버를 사용하여 진행하기를 권장합니다. 이 중 10.0.0.1은 테스트 서버이고, 10.0.0.2~10.0.0.9는 보조 트레이닝 서버입니다.

#### 테스트 서버
다음 명령어를 실행하여 네트워크 pps 값을 조회하십시오.
```
netserver
sar -n DEV 2
```

### 보조 트레이닝 서버

다음 명령어를 실행하십시오.
```
./netperf -H <테스트 서버 개인 IP 주소-l 300 -t TCP_RR -- -r 1,1 &
```
보조 트레이닝 서버는 TCP-RR 한계치에 도달하기 위해 여러 개의 netperf 인스턴스(경험상 총 netperf 인스턴스 수는 최소 300 이상 필요함)를 시작해야 합니다.
예를 들어 테스트 서버의 개인 IP 주소가 10.0.0.1일 경우에는 다음 명령어를 실행하십시오.
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## 테스트 데이터 결과 분석

### sar 툴 성능 분석

#### 데이터 분석 샘플

```
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:05 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:06 PM      eth0 1646689.00      1.00  69148.10      0.40      0.00      0.00      0.00
02:41:06 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:06 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:07 PM      eth0 1605957.00      1.00  67437.67      0.40      0.00      0.00      0.00
02:41:07 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

#### 필드 설명

| 필드    | 설명                   |
| ------- | ---------------------- |
| rxpck/s | 초당 수신량，pps 수신|
| txpck/s | 초당 발신량，pps 발신|
| rxkB/s  | 수신 대역폭               |
| txkB/s  | 발신 대역폭               |

### iperf 툴 성능 분석

#### 데이터 분석 샘플

```
	[ ID] Interval           Transfer     Bandwidth
	[  5]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  5]   0.00-300.03 sec  6.88 GBytes   197 Mbits/sec                  receiver
	[  7]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  7]   0.00-300.03 sec  6.45 GBytes   185 Mbits/sec                  receiver
	[  9]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  9]   0.00-300.03 sec  6.40 GBytes   183 Mbits/sec                  receiver
	[ 11]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 11]   0.00-300.03 sec  6.19 GBytes   177 Mbits/sec                  receiver
	[ 13]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 13]   0.00-300.03 sec  6.82 GBytes   195 Mbits/sec                  receiver
	[ 15]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 15]   0.00-300.03 sec  6.70 GBytes   192 Mbits/sec                  receiver
	[ 17]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 17]   0.00-300.03 sec  7.04 GBytes   202 Mbits/sec                  receiver
	[ 19]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 19]   0.00-300.03 sec  7.02 GBytes   201 Mbits/sec                  receiver
	[SUM]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[SUM]   0.00-300.03 sec  53.5 GBytes  1.53 Gbits/sec                  receiver
```

#### 필드 설명

SUM 행에서 sender는 데이터 발신량, receiver는 데이터 수신량을 나타냅니다.

| 필드      | 설명                                             |
| --------- | ------------------------------------------------ |
| Interval  | 테스트 시간                                         |
| Transfer  | 데이터 전송량, sender 발신량과 receiver 수신량으로 나뉩니다. |
| Bandwidth | 대역폭, sender 발송 대역폭과 receiver 수신 대역폭으로 나뉩니다.   |

## 다중 netperf 인스턴스 시작 스크립트

TCP-RR 및 UDP-STREAM에서는 여러 Netperf 인스턴스를 작동해야 할 수 있으며, 구체적으로 몇개의 인스턴스가 호스트 구성과 관련 있는지 설명합니다. 본문에서는 다중 Netperf 를 작동하는 스크립트 템플릿을 제공하여 테스트 프로세스를 간소화합니다. TCP_RR를 예로 하며, 스크립트 내용은 다음과 같습니다.
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # -H 뒤 서버 IP 주소를 입력하십시오;
     # -l 뒤는 테스트 시간으로，netperf 사전 종료를 예방하기 위해서 시간을 10000으로 설정하십시오.
     # -t 뒤는 테스트 모드로 TCP_RR 또는 TCP_CRR을 입력하십시오.
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
