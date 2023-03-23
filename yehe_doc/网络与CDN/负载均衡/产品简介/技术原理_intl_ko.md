CLB(Cloud Load Balancer)는 레이어 4(TCP, UDP 및 TCP SSL 프로토콜) 및 레이어 7(HTTP 및 HTTPS 프로토콜) 로드 밸런싱을 제공합니다. CLB를 사용하여 비즈니스 트래픽을 여러 실제 서버로 분산하여 단일 실패 지점을 제거하고 비즈니스 가용성을 보장할 수 있습니다. CLB는 클러스터 배치를 채택하여 세션 동기화를 달성하여 서버의 단일 장애 지점을 제거하고 시스템 이중화를 개선하여 서비스 안정성을 보장합니다. CLB는 도시 내 재해 복구를 구현하기 위해 동일한 리전의 여러 데이터 센터에 배포할 수 있습니다.

## 기초 아키텍처
현재 Tencent Cloud CLB는 레이어 4 및 레이어 7 로드 밸런싱 서비스를 제공합니다.
- 레이어 4에서는 통합 TGW(Tencent Gateway)를 기반으로 로드 밸런싱이 구현됩니다. TGW는 고가용성, 고확장성, 고성능 및 강력한 공격 방지 기능과 같은 기능을 가지고 있습니다. DPDK(Data Plane Development Kit) 기반의 고성능 포워딩을 지원합니다. TGW를 사용하면 단일 클러스터가 수억 개의 동시 요청과 수천만 개의 PPS(초당 패킷)를 지원할 수 있습니다. Tencent 게임, Tencent 비디오, WeChat 및 QQ와 같은 많은 Tencent 비즈니스는 서비스 액세스를 위해 TGW를 사용합니다.
- 레이어 7에서는 STGW(Secure Tencent Gateway)를 기반으로 로드 밸런싱이 구현됩니다. Tencent가 Nginx 기반으로 개발한 로드 밸런싱 서비스로 대규모 동시성을 지원합니다. Tencent 뉴스, Licaitong, Tencent 게임 및 WeChat과 같은 Tencent의 레이어 7 비즈니스 트래픽을 대량으로 전달합니다.
![](https://main.qcloudimg.com/raw/c2607a45aec0366af276f70e65722f4c.png)

## 포워딩 경로
CLB는 비즈니스 트래픽을 포워딩하고 실제 서버는 비즈니스 요청을 처리합니다. CLB는 Tencent Cloud 사설망을 통해 실제 서버와 통신합니다. TGW와 STGW는 모두 여러 서버에 배포되며 클러스터를 통해 로드 밸런싱 서비스를 제공합니다. CLB의 포워딩 경로는 다음과 같습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bzmv359_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230323115443.png)
1. TCP/UDP 프로토콜:
 - TCP/UDP 프로토콜의 포워딩 로직은 TGW 클러스터에서 처리합니다.
 - TGW는 비즈니스 트래픽을 수신한 후 Tencent Cloud의 사설망을 통해 실제 서버로 포워딩합니다. 실제 서버의 반환 패킷도 TGW를 통해 클라이언트로 반환됩니다.
2. TCP SSL 프로토콜
 - TCP SSL 프로토콜이 처리되면 비즈니스 트래픽은 TGW 클러스터를 거쳐 STGW 클러스터를 거쳐 실제 서버로 트래픽을 포워딩합니다.
 - 새 세션이 설정되기 전에 인증서 확인, 암호화, 암호 해독 및 기타 작업을 위해 가속기 카드 클러스터를 통과해야 합니다.
 - 비즈니스 트래픽이 도착하면 Tencent Cloud의 사설망을 통해 TGW, STGW, 실제 서버를 차례로 통과합니다. 반환 패킷은 역순으로 클라이언트에 전송됩니다.
3. HTTP/HTTPS 프로토콜
 - HTTP 또는 HTTPS 프로토콜이 처리될 때 비즈니스 트래픽은 TGW 클러스터를 통과한 다음 HTTP 프로토콜을 식별하고 트래픽을 실제 서버로 포워딩하는 STGW 클러스터를 통과합니다.
 - 새 HTTPS 세션이 설정되기 전에 인증서 확인, 암호화, 암호 해독 및 기타 작업을 위해 가속기 카드 클러스터를 통과해야 합니다. HTTPS는 HTTP 프로토콜로 변환된 다음 실제 서버로 포워딩됩니다.
 - 비즈니스 트래픽이 도착하면 Tencent Cloud의 사설망을 통해 TGW, STGW, 실제 서버를 차례로 통과합니다. 반환 패킷은 역순으로 클라이언트에 전송됩니다.
