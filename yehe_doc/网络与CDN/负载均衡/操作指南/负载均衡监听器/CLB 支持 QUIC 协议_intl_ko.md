[QUIC](https://www.chromium.org/quic) 프로토콜을 사용하면 네트워크가 약하거나 Wi-Fi와 4G 간의 빈번한 전환과 같은 시나리오에서 재연결이 필요 없이 App에 더 빠르게 액세스하고 다중화를 달성할 수 있습니다. 본문은 CLB 콘솔에서 QUIC 프로토콜을 구성하는 방법을 소개합니다.
## QUIC 개요
QUIC(Quick UDP Internet Connection)는 Google에서 설계한 전송 레이어 네트워크 프로토콜로 UDP를 사용하여 동시 데이터 스트림을 다중화합니다. 널리 사용되는 TCP+TLS+HTTP2 프로토콜과 비교하여 QUIC에는 다음과 같은 장점이 있습니다.
- 연결 설정 시간이 단축되었습니다.
- 혼잡 제어를 개선합니다.
- HOL(head-of-line) 차단을 피하기 위해 멀티플렉스를 채택합니다.
- 연결 마이그레이션을 지원합니다.

QUIC가 활성화되면 클라이언트는 CLB(Cloud Load Balancer) 인스턴스와 QUIC 연결을 설정할 수 있습니다. 클라이언트와 CLB 인스턴스 간의 협상으로 인해 QUIC 연결이 실패하면 HTTPS 또는 HTTP/2가 사용됩니다. 그러나 CLB 인스턴스와 리얼 서버는 여전히 HTTP1.x 프로토콜을 사용합니다.


## 사용 제한
- CLB 인스턴스만 QUIC 프로토콜을 지원합니다.
- IPv4 및 IPv6 NAT64 CLB만 QUIC 프로토콜이 지원되며 IPv6 버전은 현재 지원되지 않습니다.
- 레이어 7 HTTPS 리스너가 있는 공중망 CLB만 QUIC 프로토콜을 지원합니다.
- QUIC 프로토콜은 단일 가용존 CLB 인스턴스에만 사용할 수 있습니다.
- 지원되는 QUIC 버전: Q050, Q046, Q043, h3-29 및 h3-27.

## 작업 순서[](id:making)
1. 필요에 따라 CLB 인스턴스를 생성합니다. 자세한 내용은 [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149)를 참고하십시오.
>?CLB 인스턴스를 생성할 때 리전으로 ‘베이징’, ‘상하이’ 또는 ‘뭄바이’를 선택하고 네트워크 유형으로 ‘공중망’을 선택합니다.
>
2. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 **CLB 인스턴스 관리**를 클릭합니다.
2. ‘CLB 인스턴스 관리’ 페이지에서 **Cloud Load Balancer** 탭을 선택합니다.
3. ‘CLB’ 태그 페이지에서 ‘베이징’, ‘상하이’ 또는 ‘뭄바이’ 리전에서 생성된 공중망 CLB 인스턴스를 찾고 작업 열 아래에서 **리스너 구성**을 클릭합니다.
![]()
4. ‘리스너 관리’ 페이지의 "HTTP/HTTPS 리스너"에서 **생성**을 클릭합니다.
![]()
5. ‘리스너 생성’ 페이지에서 수신 포트의 프로토콜로 HTTPS를 선택합니다. 다른 구성을 완료하고 **제출**을 클릭합니다.
![]()
6. **리스너 관리** 탭에서 생성된 리스너 오른쪽의 **+**를 클릭합니다.
![]()
7. ‘포워딩 규칙 생성’ 페이지에서 QUIC를 활성화하고 레이어 7 규칙을 생성합니다. 관련 필드를 채우고 **다음**을 클릭하여 기본 구성을 완료합니다.
>?
>- HTTPS 포워딩 규칙을 생성할 때 QUIC 프로토콜을 활성화한 경우 나중에 필요에 따라 QUIC 프로토콜을 활성화하거나 비활성화할 수 있습니다. HTTPS 포워딩 규칙을 생성할 때 QUIC 프로토콜을 활성화하지 않은 경우 나중에 활성화할 수 없습니다.
>- UDP 프로토콜을 기반으로 QUIC는 CLB 인스턴스의 UDP 포트를 사용합니다. HTTPS 리스너에 대해 QUIC를 활성화하면 UDP 및 TCP 포트가 사용됩니다. 예를 들어 HTTPS:443 리스너에 대해 QUIC를 활성화하면 TCP:443 및 UDP:443 포트가 모두 사용되며 TCP:443 또는 UDP:443 리스너를 생성할 수 없습니다.
>
![]()

## 후속 작업
기본 구성이 완료된 후 [Health Check](https://intl.cloud.tencent.com/document/product/214/6097) 및 [Session Persistence](https://intl.cloud.tencent.com/document/product/214/6154)를 구성할 수 있습니다.

