CLB는 IPv6 인스턴스 생성을 지원하며, Tencent Cloud는 인스턴스에 IPv6 공중망 주소(IPv6 버전의 VIP)를 제공하고 해당 VIP는 IPv6 클라이언트의 요청을 포워딩합니다. 해당 기능 내부 테스트 중이고 사용해야 할 경우, [내부 테스트 신청](https://cloud.tencent.com/apply/p/qk4z8jli43)을 제출하십시오.

## IPv6이란 무엇인가요?
Ipv6이란 인터넷 프로토콜 버전 6을 가리키며 인터넷 프로토콜(IP)의 최신 버전입니다. IPv6은 IETF(Internet Engineering Task Force)가 설계한 현재 버전 IP 프로토콜(Pv4)을 대체하는 차세대 IP 프로토콜로 IPv4와 비교하였을 때 IPv6의 주요 특징은 다음과 같습니다.
- IPv6은 주소 공간이 더 큽니다. 현재 IPv4는 32자리 주소를 채택하였기 때문에 네트워크 주소 리소스가 한정적이어서 인터넷 응용과 발전을 심각하게 제약합니다. 하지만 IPv6은 128 자리 주소를 채택하였습니다. 즉, IPv6은 2<sup>128</sup>(약 3.4\*10<sup>38</sup>) 개의 주소를 지원하기 때문에 IPv4보다 약 7.9\*10<sup>28</sup>개의 주소가 증가했습니다. IPv6을 사용하면 전 세계의 작은 모래알에게도 IP 주소를 할당할 수 있습니다.
- IPv6은 더 작은 라우팅 테이블을 사용하기 때문에 라우터가 데이터 패킷을 포워딩하는 속도를 향상시켰습니다.
- IPv6은 멀티캐스트와 흐름 제어에 대한 지원을 강화하여 서비스 품질을 제어하기 위헤 우수한 네트워크 플랫폼을 제공하였습니다.
- Ipv6은 더 높은 안전성을 지니고 있습니다. IPv6 중 암호화와 감별 옵션에 그룹화의 기밀성과 완전성을 제공함으로써 네트워크의 안전성을 크게 강화하였습니다.

## IPv6 CLB 아키텍처
IPv6 CLB의 아키텍처는 다음 그림과 같습니다.
![](https://main.qcloudimg.com/raw/caae8ad5e6a49ce24aeaa3fc0a6fd0c7.svg)
IPv6 네트워크를 통해 IPv6 CLB에 접근할 때, CLB는 원활하게 IPv6 주소를 IPv4 주소로 전환하여 기존 서비스에 적응함으로써 IPv6 개조를 빠르게 구현합니다.

## IPv6 CLB 장점
Tencent Cloud CLB는 비즈니스가 IPv6에 빠르게 액세스하도록 도울 때 다음과 같은 장점을 지니고 있습니다.
- 빠른 액세스: 초 단위로 IPv6에 액세스하기 때문에 구매 즉시 사용하여 빠르게 런칭할 수 있습니다.
- 비즈니스 순조롭게 이행: 비즈니스는 클라이언트를 개조하기만 하면 백 엔드를 개조하지 않아도 IPv6에 부드럽게 액세스할 수 있습니다. IPv6 CLB는 IPv6 클라이언트로 온 접근을 지원하며, IPv6 메시지를 IPv4 메시지로 전환합니다. 백 엔드 CVM의 응용프로그램은 IPv6을 감지하지 않아도 기존 형식으로 작업을 배포할 수 있습니다.
- 사용하기 편리함: IPv6 CLB는 기존 IPv4 CLB의 작업 트래픽을 호환하기 때문에 학습 비용이 제로이며 사용하기 매우 쉽습니다.

>!
>- 현재 IPv6 CLB는 베이징, 상하이, 광저우 세 지역만 지원합니다.
>- IPv6 CLB는 **응용형** CLB만 지원하며 전통형 CLB는 지원하지 않습니다.
>- 인터넷 IPv6 네트워크 환경은 구축 초기에 처하므로 회선 접근 불통 상황이 발생할 경우, [티켓](https://console.cloud.tencent.com/workorder/category)을 입력하여 피드백하십시오. 또한 내부 테스트 기간에는 SLA 보장을 제공하지 않습니다.


## 작업 가이드
### IPv6 CLB 생성
1. Tencent Cloud 공식 사이트에 로그인하여 [CLB 구매 페이지](https://buy.cloud.tencent.com/lb)에 진입합니다.
2. 인스턴스 유형은 **응용형 CLB**를, IP 유형은 **IPv6**을 선택합니다. 기타 구성은 일반 인스턴스 구성과 동일합니다.
3. 구매 완료 후, [CLB 인스턴스 목록 페이지](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)로 돌아가고 구매한 IPv6 CLB를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/1b87146cc6b4e42417e2d323f4f6d00c.png)

### IPV6 CLB 사용
[CLB 관리 콘솔](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1)에 로그인하고 인스턴스 ID를 클릭하여 세부 정보 페이지에 진입하여 **수신기 관리** 페이지에서 수신기, 포워딩 규칙, CVM 바인딩을 구성합니다. 세부 정보는 [응용형 LB 시작 가이드](https://cloud.tencent.com/document/product/214/8975)를 참조하십시오.
![](https://main.qcloudimg.com/raw/9802a8e3baeffccb1b1ba853594b0755.png)

