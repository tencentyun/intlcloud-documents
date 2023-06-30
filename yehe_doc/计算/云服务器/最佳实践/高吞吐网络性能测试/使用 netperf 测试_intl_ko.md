## 작업 시나리오
본문은 netperf 방법을 사용하여 높은 처리량의 CVM 네트워크 성능을 테스트하는 방법을 설명합니다.

## 툴 소개
- Netperf
HP에서 개발한 네트워크 성능 측정 툴로서, 주로 TCP 및 UDP의 처리량 성능을 테스트합니다. 테스트 결과는 주로 시스템에서 다른 시스템으로 데이터를 발송하는 속도와 다른 시스템이 데이터를 수신하는 속도를 반영합니다.
- SAR
네트워크 트래픽을 모니터링하는 데 사용되며, 실행 예시는 다음과 같습니다.
```
sar -n DEV 1
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
``` 
필드 해석은 다음과 같습니다.
<table>
<thead>
<tr>
<th>필드</th>
<th>단위</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>rxpck/s</td>
<td>pps</td>
<td>초당 수신된 패킷량, 즉 수신 pps</td>
</tr>
<tr>
<td>txpck/s</td>
<td>pps</td>
<td>초당 전송된 패킷량, 즉 발신 pps</td>
</tr>
<tr>
<td>rxkB/s</td>
<td>kB/s</td>
<td>수신 대역폭</td>
</tr>
<tr>
<td>txkB/s</td>
<td>kB/s</td>
<td>발신 대역폭</td>
</tr>
</tbody></table>


## 테스트 시나리오 및 성능 지표

### 테스트 시나리오[](id:multiSceneTest)
<table>
<tr>
<th width="13%">테스트 시나리오</th>
<th width="75%">클라이언트 실행 명령</th>
<th>SAR 모니터링 지표</th>
</tr>
<tr>
<td>UDP 64</td>
<td><code>netperf -t UDP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 64 -R 1 &</code></td>
<td>PPS</td>
</tr>
<tr>
<td>TCP 1500</td>
<td><code>netperf -t TCP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 1500 -R 1 &</code></td>
<td>대역폭</td>
</tr>
<tr>
<td>TCP RR</td>
<td><code>netperf -t TCP_RR -H &lt;server ip&gt; -l 10000 -- -r 32,128 -R 1 &</code></td>
<td>PPS</td>
</tr>
</table>

### 성능 지표[](id:Performance)
<table>
<thead>
<tr>
<th>지표</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>64바이트 UDP 수발신 PPS(패킷/초)</td>
<td>UDP를 통한 데이터 배치 발송 처리량을 나타내며, 이는 네트워크의 최대 전달 능력(패킷 손실이 발생할 수 있음)을 반영합니다. </td>
</tr>
<tr>
<td>1500바이트 TCP 수발신 대역폭(Mbits/초)</td>
<td>TCP를 통한 데이터 배치 발송 처리량을 나타내며, 이는 네트워크의 최대 대역폭 성능(패킷 손실이 발생할 수 있음)을 반영합니다. </td>
</tr>
<tr>
<td>TCP-RR(회/초)</td>
<td>TCP 지속 연결 중에 Request/Response 작업을 반복하는 트랜잭션 처리량을 나타내며, 이는 패킷 손실 없는 TCP의 네트워크 전송 능력을 반영합니다. </td>
</tr>
</tbody></table>

## 작업 순서
### 테스트 환경 준비
1. 테스트 서버 3대를 준비합니다. [사용자 정의 Linux CVM 설정](https://intl.cloud.tencent.com/document/product/213/10517)을 참고하여 테스트 서버를 구매합니다. 본문의 테스트 서버는 CentOS 8.2 운영 체제를 사용합니다.
2. 테스트 서버에 순서대로 로그인하고 다음 명령을 실행하여 netperf 툴을 다운로드합니다. CVM에 로그인하는 방법은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget -O netperf-2.7.0.tar.gz -c  https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.7.0
```
```
tar zxf netperf-2.7.0.tar.gz
```
```
cd netperf-netperf-2.7.0
```
```
./autogen.sh && ./configure && make && make install
```

### 송신 패킷 성능 테스트
1. [](id:Step1) 디바이스에서 다음 명령을 실행하여, 나머지 netperf 및 netserver 프로세스를 중지합니다.
```
pkill netserver && pkill netperf
```
2. 디바이스 a를 클라이언트로, 디바이스 b와 c를 서버로 사용합니다. 서버에서 다음 명령을 실행하여 netserver를 실행합니다.
```
netserver
```
 - 반환 결과가 아래 이미지와 같으면 아직 다른 netserver 프로세스가 있음을 의미합니다. [1단계](#Step1)의 명령을 실행하여 프로세스를 중지합니다.
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - 반환 결과가 아래 이미지와 같으면 netserver가 성공적으로 실행되었음을 의미하므로 다음 단계를 진행합니다.
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. 클라이언트에서 [테스트 시나리오](#multiSceneTest)에 제공된 명령을 실행하고, 클라이언트의 패킷 발송 성능이 더 이상 증가하지 않을 때까지 netperf 프로세스를 계속 늘리거나 줄입니다.
>?명령을 반복 실행하고 server IP는 다른 서버 IP를 사용해야 합니다. 프로세스가 최대 성능에 도달하지 못하는 경우 [테스트 보조 스크립트](#auxiliaryScript)를 실행하여 프로세스를 일괄 실행할 수 있습니다.
>
4. 클라이언트에서 다음 명령을 실행하여 클라이언트의 패킷 전송 성능 변화를 모니터링하고 최대값을 얻습니다.
```
sar -n DEV 1
```
얻어진 결과에 따라 [성능 지표](#Performance)를 참고하여 분석을 진행하고, 높은 처리량의 CVM 네트워크의 성능을 측정합니다.

### 수신 패킷 테스트
1. [](id:StepOne) 디바이스에서 다음 명령을 실행하여 나머지 netperf 및 netserver 프로세스를 중지합니다.
```
pkill netserver && pkill netperf
```
2. 디바이스 a를 서버로, 디바이스 b와 c를 클라이언트로 사용합니다. 서버에서 다음 명령을 실행하여 netserver를 실행합니다.
```
netserver
```
 - 반환 결과가 아래 이미지와 같으면 아직 다른 netserver 프로세스가 있음을 의미합니다. 프로세스를 중지하려면 [1단계](#StepOne)의 명령을 실행하십시오.
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - 반환 결과가 아래 이미지와 같으면 netserver가 성공적으로 실행되었음을 의미하므로 다음 단계를 진행합니다.
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. 클라이언트에서 [테스트 시나리오](#multiSceneTest)에 제공된 명령을 실행하고, 클라이언트의 패킷 발송 성능이 더 이상 증가하지 않을 때까지 netperf 프로세스를 계속 늘리거나 줄입니다.
>?명령을 반복 실행하고 각각의 클라이언트에서 netperf를 전송합니다. 프로세스가 최대 성능에 도달하지 못하는 경우 [테스트 보조 스크립트](#auxiliaryScript)를 실행하여 프로세스를 일괄 실행할 수 있습니다.
>
4. 클라이언트에서 다음 명령을 실행하여 클라이언트의 패킷 전송 성능 변화를 모니터링하고 최대값을 얻습니다.
```
sar -n DEV 1
```
얻어진 결과에 따라 [성능 지표](#Performance)를 참고하여 분석을 진행하고, 높은 처리량의 CVM 네트워크의 성능을 측정합니다.

## 부록

### 테스트 보조 스크립트 [](id:auxiliaryScript)
이 스크립트를 실행하면 여러 netperf 프로세스를 빠르게 전달할 수 있습니다.
```
#!/bin/bash
count=$1
for ((i=1;i<=count;i++))
do
    echo "Instance:$i-------"
    # 아래 명령은 테스트 시나리오 테이블의 명령으로 대체할 수 있습니다.
    # -H 뒤에 서버 IP 주소를 입력합니다.
    # -l 뒤는 테스트 시간으로，netperf 사전 종료를 방지하기 위해 시간을 10000으로 설정하십시오.
    netperf -t UDP_STREAM -H <server ip> -l 10000 -- -m 64 -R 1 &
done
```
