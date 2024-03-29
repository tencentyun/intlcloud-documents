CLB는 주로 다음 시나리오에 적합합니다.
- 트래픽 분포. CLB는 다수의 액세스 요청이 있는 비즈니스 트래픽을 여러 CVM 인스턴스에 분산할 수 있습니다.
- 단일 실패 지점 제거. 일부 CVM 인스턴스를 사용할 수 없게 되면 CLB가 자동으로 차단하여 애플리케이션 시스템의 정상적인 작동을 보장할 수 있습니다.
- 수평적 확장성. 필요에 따라 애플리케이션 시스템의 서비스 기능을 확장할 수 있으며 이는 Web Server 및 App Server에 적합합니다.
- 글로벌 로드 밸런싱. 원격 재해 복구를 보장하는 글로벌 다중 리전 로드 밸런싱을 지원합니다.

## 단일 장애 지점의 트래픽 분산 및 제거
CLB를 사용하여 비즈니스 트래픽을 여러 CVM 인스턴스에 배포할 수 있습니다.
- 비즈니스 클라이언트가 CLB에 액세스합니다.
- 여러 CVM 인스턴스는 CLB가 비즈니스 트래픽을 포워딩하는 고성능 및 고가용성 서비스 풀을 형성합니다.
- 하나 이상의 CVM 인스턴스를 사용할 수 없게 되면 CLB가 자동으로 해당 인스턴스를 차단하고 요청을 일반 CVM 인스턴스에 배포하여 애플리케이션 시스템의 작동을 보장할 수 있습니다.
- 비즈니스가 여러 가용존에 배포된 경우 실제 서버 레이어에서 다중 가용존 재해 복구를 보장하기 위해 CLB 인스턴스를 여러 가용존의 CVM 인스턴스에 동시에 바인딩하는 것이 좋습니다.
- 세션 지속성 기능은 동일한 클라이언트의 요청을 동일한 실제 서버로 포워딩할 수 있어 액세스 효율성이 향상됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/af522691e22caa4cc6160a7fe17880d8.svg)

## 수평적 확장성
[Auto Scaling](https://intl.cloud.tencent.com/document/product/377)을 사용하면 CLB가 비즈니스 요구 사항에 따라 CVM 인스턴스를 자동으로 생성하고 릴리스할 수 있습니다.
- Auto Scaling 정책을 구성하여 CVM 인스턴스 수를 관리하고, 인스턴스 환경을 배포하고, 비즈니스 운영을 보장할 수 있습니다. CLB는 수요가 최고조에 달할 때 자동으로 CVM 인스턴스를 추가하여 고성능을 유지하고, 수요가 감소하면 비용을 절감하기 위해 CVM 인스턴스를 제거할 수 있습니다.
- 예를 들어 ‘블랙 프라이데이’와 같은 전자상거래의 주요 판매 캠페인 중에 Web 트래픽이 갑자기 10배 증가할 수 있으며 몇 시간 동안만 지속됩니다. 이 경우 CLB와 AS를 사용하여 IT 비용 절감을 극대화할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/38d3f5c690ecb3344e75af20431d5986.svg)

## 글로벌 로드 밸런싱
DNSPod와 결합된 CLB를 사용하면 비즈니스 트래픽을 다양한 리전의 글로벌 로드 밸런싱으로 해결할 수 있어 원격 멀티 사이트 활성-활성 및 재해 복구를 보장합니다.
- 다른 리전에 CLB 인스턴스를 배포하고 해당 리전의 CVM 인스턴스에 바인딩할 수 있습니다.
- DNSPod를 사용하여 다양한 리전의 CLB VIP에 대한 도메인 이름을 확인할 수 있습니다.
- 비즈니스 트래픽은 DNS 및 CLB를 통해 여러 리전의 여러 CVM 인스턴스로 포워딩되어 글로벌 로드 밸런싱을 구현합니다.
- 리전을 사용할 수 없게 되면 해당 리전에서 CLB VIP의 리졸브를 일시 중단하여 비즈니스에 영향을 미치지 않도록 할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5a71a839a2aa222e16b878e28c26c7db.svg)


