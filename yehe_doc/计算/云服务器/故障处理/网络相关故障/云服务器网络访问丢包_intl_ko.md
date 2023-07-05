본문은 CVM 네트워크 액세스 패킷 손실 문제를 일으킬 수 있는 주요 원인과 문제 진단 및 솔루션을 소개합니다.

## 예상 원인
CVM 네트워크 액세스의 패킷 손실 문제에 대한 예상 원인은 다음과 같습니다.
- [속도 제한 트리거로 인한 TCP 패킷 손실](#tcpPacketLoss)
- [속도 제한 트리거로 인한 UDP 패킷 손실](#udpPacketLoss)
- [소프트웨어 인터럽트 패킷 손실 트리거](#softInterrupt)
- [UDP 전송 버퍼 가득 참](#sendBuffer)
- [UDP 수신 버퍼 가득 참](#receiveBuffer)
- [TCP 완전 연결 큐 가득 참](#tcpFullyConnectedQueue)
- [TCP 요청 오버플로](#tcpRequestOverflow)
- [연결 수 상한 도달](#upperLimit)
- [iptables policy 설정 관련 규칙](#iptablesPolicy)


## 전제 조건
문제 파악 및 해결 전, 인스턴스에 로그인해야 하며, 자세한 내용은 [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/zh/document/product/213/32493) 및 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/zh/document/product/213/32495)을 참고하십시오.

## 장애 처리

### 속도 제한 트리거로 인한 TCP 패킷 손실[](id:tcpPacketLoss)
CVM 인스턴스에는 여러 사양이 있으며 사양마다 네트워크 성능이 다릅니다. 인스턴스의 대역폭 또는 패킷량이 인스턴스 사양 해당 기준을 초과하면 플랫폼 측의 속도 제한이 트리거되어 패킷 손실이 발생합니다. 문제 진단 및 해결 절차는 다음과 같습니다.
1. 인스턴스의 대역폭과 패킷량을 확인합니다.
Linux 인스턴스는 `sar -n DEV 2` 명령을 실행하여 대역폭과 패킷량을 확인할 수 있습니다. 이 중 `rxpck/s`와 `txpck/s` 지표는 송수신 패킷량이고 `rxkB/s`와 `txkB/s`의 지표는 송수신 대역폭입니다.
2. 획득한 대역폭 및 패킷량 데이터를 [인스턴스 스펙](https://intl.cloud.tencent.com/document/product/213/11518)과 비교하여 인스턴스 사양의 성능 병목 지점에 도달했는지 확인합니다.
 - 확인 결과 맞는 경우, 인스턴스 사양을 업그레이드하거나 서비스량을 조정해야 합니다.
 - 확인 결과 아닌 경우, [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category
)을 통해 추가적인 문제 파악 및 해결을 진행하실 수 있습니다.

### 속도 제한 트리거로 인한 UDP 패킷 손실[](id:udpPacketLoss)
[속도 제한 트리거로 인한 TCP 패킷 손실](#tcpPacketLoss) 절차를 참고하여 인스턴스 사양 성능 병목 현상으로 인한 패킷 손실인지 확인합니다.
 - 확인 결과 맞는 경우, 인스턴스 사양을 업그레이드하거나 서비스량을 조정해야 합니다.
 - 확인 결과 아닌 경우, DNS 요청에 대한 플랫폼의 추가 주파수 제한이 원인일 수 있습니다. 인스턴스의 전체 대역폭 또는 패킷량이 인스턴스 사양의 성능 병목 지점에 도달하면 DNS 요청 속도 제한이 트리거되어 UDP 패킷 손실이 발생할 수 있습니다. [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 처리하시기 바랍니다.


### 소프트웨어 인터럽트 패킷 손실 트리거[](id:softInterrupt)
운영 체제가 `/proc/net/softnet_stat`의 두 번째 열에 있는 카운트 값이 증가하는 것을 감지하면 "소프트웨어 인터럽트 패킷 손실"로 판단합니다. 인스턴스가 소프트웨어 인터럽트 패킷 손실을 트리거하면 다음 절차를 통해 문제를 진단 및 해결할 수 있습니다. 
RPS 활성화 여부 확인:
 - 활성화됨: 커널 매개변수 `net.core.netdev_max_backlog`가 너무 작으면 패킷 손실이 발생하므로 상향 조정해야 합니다. 커널 매개변수에 대한 자세한 내용은 [Linux 인스턴스 상용 커널 매개변수 소개](https://intl.cloud.tencent.com/document/product/213/39162)를 참고하십시오.
 - 미활성화: CPU 단일 코어 소프트웨어 인터럽트가 높아서 데이터를 제때 송수신하지 못하는지 확인하십시오. 맞다면 다음을 진행합니다.
  - RPS를 활성화하여 소프트웨어 인터럽트를 보다 균형적으로 분배합니다.
  - 작업 프로그램으로 인해 소프트웨어 인터럽트 분배가 불균형적인지 확인하십시오.

### UDP 전송 버퍼 가득 참[](id:sendBuffer)
UDP 버퍼가 충분하지 않아 인스턴스에서 패킷이 손실되는 경우 다음 절차에 따라 문제를 진단 및 해결할 수 있습니다.
1. `ss -nump` 명령어를 통해 UDP 전송 버퍼가 가득 찼는지 확인합니다.
2. 확인 결과 맞는 경우, 커널 매개변수 `net.core.wmem_max` 및 `net.core.wmem_default`를 늘리고 UDP 프로그램을 다시 시작하여 적용하십시오. 커널 매개변수에 대한 자세한 내용은 [Linux 인스턴스 상용 커널 매개변수 소개](https://intl.cloud.tencent.com/document/product/213/39162)를 참고하십시오.
3. 여전히 패킷 손실 문제가 있는 경우 `ss -nump` 명령어를 통해 전송 버퍼가 예상대로 증가하지 않았는지 확인합니다. 이때 setsockopt를 통해 서비스 코드에 SO_SNDBUF를 설정했는지 확인하고, 맞다면 코드를 수정하여 SO_SNDBUF를 늘리십시오.

### UDP 수신 버퍼 가득 참[](id:receiveBuffer)
UDP 버퍼가 충분하지 않아 인스턴스에서 패킷이 손실되면 다음 절차에 따라 처리할 수 있습니다.
1. `ss -nump` 명령어를 통해 UDP 수신 버퍼가 가득 찼는지 확인합니다.
1. 확인 결과 맞는 경우, 커널 매개변수 `net.core.rmem_max` 및 `net.core.rmem_default`를 늘리고 UDP 프로그램을 다시 시작하여 적용하십시오. 커널 매개변수에 대한 자세한 내용은 [Linux 인스턴스 상용 커널 매개변수 소개](https://intl.cloud.tencent.com/document/product/213/39162)를 참고하십시오.
2. 패킷 손실 문제가 있는 경우 `ss -nump` 명령어를 통해 수신 버퍼가 예상대로 증가하지 않았는지 확인합니다. 이때 setsockopt를 통해 서비스 코드에 SO_RCVBUF를 설정했는지 확인하고, 맞다면 코드를 수정하여 SO_RCVBUF를 늘리십시오.

### TCP 완전 연결 큐 가득 참[](id:tcpFullyConnectedQueue)
TCP 완전 연결 큐의 길이는 'net.core.somaxconn'와 서비스 프로세스 호출 listen 시 전달되는 backlog 매개변수 중 더 작은 값을 취합니다. 인스턴스의 TCP 완전 연결 큐가 가득 차서 패킷 손실이 발생하면 다음 절차에 따라 해결할 수 있습니다.
1. 커널 매개변수 `net.core.somaxconn`을 늘립니다. 커널 매개변수에 대한 자세한 내용은 [Linux 인스턴스 상용 커널 매개변수 소개](https://intl.cloud.tencent.com/document/product/213/39162)를 참고하십시오.
2. backlog 매개변수가 서비스 프로세스에서 전달되는지 확인합니다. 그렇다면 상향 조정하십시오.

### TCP 요청 오버플로[](id:tcpRequestOverflow)
TCP가 데이터를 수신할 때 socket이 user에 의해 잠겨 있으면 데이터가 backlog 큐로 전송됩니다. 이 프로세스가 실패하면 TCP 요청 오버플로 및 패킷 손실이 발생합니다. 작업 프로그램 성능이 정상이라면, 다음 절차를 통해 시스템 수준에서 문제를 진단 및 해결할 수 있습니다.

작업 프로그램이 setsockopt를 통해 buffer 크기를 자체 설정했는지 확인합니다.
- 확인 결과 맞는 경우, 또한 해당 설정 값이 충분히 크지 않은 경우, 더 큰 값으로 수정하여 더 이상 setsockopt를 통해 크기가 지정되지 않도록 합니다.
<dx-alert infotype="explain" title="">
setsockopt의 값은 커널 매개변수 `net.core.rmem_max` 및 `net.core.wmem_max`에 의해 제한됩니다. 작업 프로그램을 조정하면서 `net.core.rmem_max`와 `net.core.wmem_max`를 동시에 조정합니다. 조정 후 작업 프로그램을 재부팅하여 설정이 적용되도록 하십시오.
</dx-alert>
- 확인 결과 아닌 경우, `net.ipv4.tcp_mem`, `net.ipv4.tcp_rmem`, 및 `net.ipv4.tcp_wmem` 커널 매개변수를 상향 조절하여 TCP socket 수위를 조정합니다.
커널 매개변수 수정에 대한 자세한 내용은 [Linux 인스턴스 상용 커널 매개변수 소개](https://intl.cloud.tencent.com/document/product/213/39162)를 참고하십시오.

### 연결 수 상한 도달[](id:upperLimit)
CVM 인스턴스에는 다양한 사양이 있으며 각 사양마다 연결 수 성능 지표가 다릅니다. 인스턴스 연결 수가 인스턴스 사양에 해당하는 기준을 초과하면 플랫폼 속도 제한이 트리거되어 패킷 손실이 발생합니다. 해결 절차는 다음과 같습니다.
<dx-alert infotype="explain" title="">
연결 수는 호스트에 저장된 CVM 인스턴스의 세션 수를 나타내며, TCP, UDP, ICMP를 포함합니다. 이 값은 CVM 인스턴스에서 `ss` 또는 `netstat` 명령어를 통해 얻은 네트워크 연결 수보다 큽니다.
</dx-alert>

인스턴스 연결 수를 확인하고, [인스턴스 스펙](https://intl.cloud.tencent.com/document/product/213/11518)과 비교하여 인스턴스 사양의 성능 병목 지점에 도달했는지 확인합니다.
 - 확인 결과 맞는 경우, 인스턴스 사양을 업그레이드하거나 서비스량을 조정해야 합니다.
 - 확인 결과 아닌 경우, 인스턴스 사양의 성능 병목 지점에 도달하지 않은 경우 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 처리하시기 바랍니다.


### iptables policy 설정 관련 규칙[](id:iptablesPolicy)
CVM의 iptables에 관련 규칙이 설정되어 있지 않은 경우, iptables policy 관련 규칙 설정으로 인해 CVM에 도달하는 모든 패킷이 버려질 수 있습니다. 처리 단계는 다음과 같습니다.

1. [](id:Step1)다음 명령을 실행하여 iptables policy 규칙을 확인합니다.
```
iptables -L | grep policy 
```
iptables policy 규칙의 기본값은 ACCEPT입니다. INPUT 체인 policy가 ACCEPT가 아니면 서버에 대한 모든 패킷이 버려집니다. 예를 들어 다음 결과가 반환되면 CVM에 들어오는 모든 패킷이 drop된다는 표시입니다.
```
Chain INPUT (policy DROP)
Chain FORWARD (policy ACCEPT)
Chain OUTPUT (policy ACCEPT)
```
2. 다음 명령을 실행하여 필요에 따라 `-P` 이후의 값을 조정합니다.
```
iptables -P INPUT ACCEPT 
```
조정 후 다시 [Step 1](#Step1) 명령을 실행하여 확인할 수 있으며 다음과 같은 결과가 반환되어야 합니다.
```
Chain INPUT (policy ACCEPT)
Chain FORWARD (policy ACCEPT)
Chain OUTPUT (policy ACCEPT)
```



