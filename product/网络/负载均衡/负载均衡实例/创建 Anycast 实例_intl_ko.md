CLB는 Anycast CLB(아래 문장에는 Anycast CLB라고 함) 인스턴스 생성을 지원합니다. Anycast CLB는 글로벌 동적 가속을 지원하는 CLB 서비스로, CLB의 VIP는 세계 여러 지역에 발포됩니다. 클라이언트는 가장 가까운 POP 액세스 포인트에 액세스하며 Tencent Cloud IDC 고속 인터넷을 통해 CVM에 포워딩됩니다.
Anycast CLB는 네트워크 전송 품질 최적화와 멀티 입구를 가까운 포인트로 액세스를 실현하여 지터, 패킷 손실을 줄임으로써 Tencent Cloud 응용프로그램의 서비스 품질을 향상시키고 서비스 범위를 확대하며 백 엔드 배포를 간소화합니다. 본 기능 내부 테스트 중이고 필요할 경우 [내부 테스트 신청](https://cloud.tencent.com/act/apply/aia)을 제출하십시오.

## Anycast란 무엇인가요?
Anycast(애니캐스트라고도 함)는 동일 IP가 여러 지역에서 동시 라우팅을 발포하는 것을 의미하며 라우팅 알고리즘은 사용자 트래픽을 가장 가까운 라우터에 배달합니다.
Anycast CLB 장점은 다음과 같습니다.
- **저지연**
Anycast CLB는 Anycast 방식을 이용해 VIP를 동시에 여러 지역으로 배포합니다. 요청 패킷은 전송 프로토콜에 따라 최적의 VIP 배포 지역에 도달하여 우선 Tencent Cloud에 진입합니다. 그 다음 Tencent Cloud의 사설망을 통해 CVM에 도착하고 공중망 혼잡을 피해 지연 시간을 줄일 수 있습니다.
- **지터와 패킷 손실 줄이기**
예를 들어 ISP 간, 국경간 문제로 공용 네트워크 링크의 성능이 불안정하면 네트워크 지터를 초래하여 서버 체험에 영향을 미칠 수 있습니다. Anycast CLB는 전송 성능이 안정적이고 가장 가까운 포인트에서 클라이언트 요청을 Tencent Cloud에 액세스를 Tencent Cloud의 사설망 직접 연결을 통해 지역 간 전송을 보장해 공중망 지터와 패킷 손실 문제를 해결해줍니다.
- **높은 신뢰성**
공중망 전송은 신뢰할 수 없으며 ISP 회선 중단으로 서비스에 대한 액세스 불가가 초래되면 사용자는 일반적으로 복구를 기다릴 수 밖에 없습니다. Anycast CLB를 사용하면 Tencent Cloud 사설망, ISP 네트워크, Tencent Cloud POP 노드를 통해 네트워크 멀티 경로와 멀티 입구를 구현해 단일 지역과 단일 회선의 고장을 차단하고 네트워크 안정성을 높입니다.
- **매포 간소화**
클라이언트가 여러 지역에 분산되어 있고 근처 노드를 통해 액세스해야 하는 서비스의 경우 여러 지역으로 배포된 기기가 필요하고 DNS를 구성하여 로드 밸런싱을 구현해야 하며 서로 다른 지역의 IP가 달라야 하기 때문에 배포가 번거롭습니다. Anycast CLB를 사용한 후 IP 측에서 지역 속성을 수렴해 각각의 지역에서 모두 IP를 구성할 필요가 없습니다. 또한 백 엔드에서 한 세트의 로직을 유지보수하면 되기 때문에 각 지역 요청을 사설망을 통해 백 엔드 기기로 빠르게 전달할 수 있습니다.

## Anycast CLB 아키텍처
Anycast CLB의 아키텍처는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/08a51e333f26f4b123703dfb7922fc68.svg)
Anycast CLB의 VIP는 전 세계 여러 지역에 배포되며 클라이언트는 가장 가까운 POP 액세스 포인트에 액세스하고 Tencent Cloud 사설망을 통해 접근 트래픽을 빠르게 CVM에 포워딩할 수 있습니다.

### Anycast 게시 지역
Anycast 게시 지역은 가속 IP 주소를 게시한 지역입니다. 즉 Anycast CLB의 VIP가 게시한 POP 액세스 포인트이고 클라이언트가 액세스한 가장 가까운 POP 액세스 포인트를 가리킵니다. 현재 Anycast CLB는 다음 게시 지역을 지원합니다.
- 게시 지역 A: 주로 중국와 유럽, 미국 지역으로 VIP는 베이징, 상하이, 광저우, 중국 홍콩, 토론토, 실리콘 밸리, 프랑크푸르트, 버지니아 및 모스크바에 동시 게시될 예정입니다.
- 게시 지역 B: 주로 중국과 동남아 지역으로 VIP는 베이징, 상하이, 광저우, 중국 홍콩, 싱가포르, 서울, 뭄바이, 방콕 및 도쿄에 동시 게시될 예정입니다.

### Anycast CLB 소속 지역
일반 CLB의 지역 개념과 같고, Anycast CLB 소속 지역은 Anycast CLB를 구매할 때 선택한 지역이자 백 엔드 CVM이 소재한 지역을 가리킵니다. 현재 Anycast CLB는 대부분의 지역을 커버하고 있습니다.
- 중국: 베이징, 상하이, 광저우, 홍콩
- 유럽과 미국: 토록토, 실리콘 밸리, 프랑크푸르트, 버지니아, 모스크바
- 동남아: 싱가포르, 서울, 뭄바이, 방콕, 도쿄
>!
>- Anycast CLB는 **응용형** CLB만 지원하며 전통형 CLB는 지원하지 않습니다.
>- Anycast CLB는 현재 **4계층 프로토콜(TCP/UDP)**만 지원하며 7계층 프로토콜(HTTP/HTTPS)은 지원하지 않습니다.
>- Anycast CLB는 S4, SN3ne, S2ne, M4, GN6s CVM을 지원하지 않습니다.


## Anycast CLB 적용 시나리오
### 글로벌 동일 서버
게임 클라이언트가 전 세계 여러 지역의 플레이어들이 동일한 지역에 있고(또는 전 세계 각지에 지사가 있는 기업이 동일한 데이터 센터를 사용하길 원할 경우) 백 엔드 서비스를 하나의 지역(예: 광저우)에 배포하시길 원합니다. 광저우 지역의 Anycast CLB를 구매한 뒤 필요에 따라 게시 지역을 선택할 수 있습니다. 전 세계 플레이어(또는 지원)가 가까운 포인트에 액세스하며 동일한 백 엔드 서비스에 접근하게 됩니다.
![](https://main.qcloudimg.com/raw/ec37cb1cdfce0cdee1bbc60598558e4c.svg)

### 게임 가속화
Anycast CLB는 게임 가속에도 중요한 역할을 하고 있습니다. 게임 요청은 가까운 노드를 통해 Tencent Cloud에 액세스하여 Tencent Cloud의 사설망 직접 연결을 통해 게임 서버에 도달하고 대폭 단축된 공중망 경로를 통해 시간 지연, 지터, 패킷 손실 등 문제를 감소시킵니다. 기존의 가속과 비교해 입구에서 별도의 트래픽을 수신하는 장치가 필요없고 지역을 구분할 필요가 없어 DNS 구성을 간이화합니다.
![](https://main.qcloudimg.com/raw/172c214c17258a279856a7e4ea0c2200.svg)


## 작업 가이드
### Anycast CLB 인스턴스 생성
1. Tencent Cloud 공식 사이트에 로그인하여 [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)에 진입합니다.
2. 인스턴스 유형을 **응용형 CLB**로 선택하고 가속 IP에서 [Anycast 가속 IP 사용]을 선택합니다. 나머지는 [일반 인스턴스 구성](https://cloud.tencent.com/document/product/214/8975#2.-.E8.B4.AD.E4.B9.B0.E5.B9.B6.E9.85.8D.E7.BD.AE.E5.85.AC.E7.BD.91.E5.BA.94.E7.94.A8.E5.9E.8Blb)과 동일합니다.
3. 구매 완료 후, [CLB 인스턴스 목록 페이지](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)로 돌아가고 구매한 Anycast CLB를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/4eac4325d24c4138daf2c46704672851.png)

### Anycast CLB 사용
1. [CLB 관리 콘솔](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)에 로그인하여 "LB 인스턴스 목록"에 진입합니다.
2. 인스턴스 ID를 클릭하여 세부 정보 페이지에 진입합니다.
3. **수신기 관리** 페이지에서 수신기를 구성하며 포워딩 규칙을 설정하고, CVM을 바인딩할 수 있습니다. 세부 정보는 [응용형 LB 시작 가이드](https://cloud.tencent.com/document/product/214/8975)를 참조하십시오.
![](https://main.qcloudimg.com/raw/a884a2e0a51cecf5056ca6053c9c2da5.png)

