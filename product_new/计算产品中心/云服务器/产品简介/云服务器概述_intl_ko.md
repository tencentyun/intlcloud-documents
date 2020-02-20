클라우드 가상 머신(Cloud Virtual Machine)은 Tencent Cloud가 제공하는 확장 가능한 컴퓨팅 서비스입니다. 기존 서버를 사용 시 리소스 용량과 초기 투자를 예측해야 했지만, CVM을 사용하는 경우에는 이런 상황을 피할 수 있습니다. 단기간에 여러 클라우드 가상 머신을 빠르게 실행하고 애플리케이션을 즉시 배포합니다.
Tencent Cloud CVM의 적용으로, CPU/메모리/디스크/네트워크/보안 등의 사용자 지정 리소스를 지원하며 필요에 따라 쉽게 조정할 수 있습니다.

## 개념

텐센트 클라우드 서버 CVM을 사용하기 전에 다음 개념에 대한 숙지가 필요합니다.
- **인스턴스**: 클라우드의 가상 컴퓨팅 리소스입니다. CPU, 조작 시스템, 네트워크, 디스크 등 컴퓨팅 구성 요소를 포함합니다.
- **인스턴스 유형** Tencent Cloud가 제공하는 CVM의 다양한 CPU, 메모리, 스토리지와 네트워크 사양입니다. [인스턴스 스펙](http://intl.cloud.tencent.com/document/product/213/11518)을 참조하면 자세한 내용을 확인할 수 있습니다.
- **미러 이미지**: 클라우드 가상 머신 CVM이 실행하는 사전 구축 템플릿입니다. 미리 설정하는 운영 체제와 소프트웨어를 포함합니다. Tencent Cloud CVM은 윈도스, 리눅스 등 다양한 사전 구축 미러 이미지를 제공합니다.
- **로컬 디스크**: 인스턴스와 같은 물리 서버에 위치합니다. 인스턴스에 의해 지속해서 저장하는 장치로 활용합니다.
- **클라우드 디스크**: 분산형의 지속적인 블록 스토리지 장치를 제공하며, 이는 인스턴스의 시스템 디스크 혹은 확장 가능한 데이터 디스크로 활용합니다.
- **사설 네트워크**: Tencent Cloud가 제공하는 격리된 가상의 네트워크 공간입니다. 다른 리소스 로직과 격리되었습니다.
– **IP주소**：Tencent Cloud는 [개인 IP](http://intl.cloud.tencent.com/document/product/213/5225)와 [공용 IP](http://intl.cloud.tencent.com/document/product/213/5224)를 제공합니다. 개인 IP는 LAN 서비스를 제공하고, 클라우드 가상 머신은 상호 액세스 가능합니다. 공용 IP의 경우, 사용자는 클라우드 가상 머신의 인스턴스에서 인터넷 서비스를 액세스할 때 사용합니다.
– **EIP**: 동적 네트워크 사용자 정의로 제작된 정적 공용 IP입니다. 오류를 빠르게 조치합니다.
- **보안 그룹**: 보안 그룹은 가상 방화벽으로 이해할 수 있습니다. 상태를 점검하고 데이터 패킷을 필터링합니다. 단일 혹은 멀티 CVM 네트워크를 액세스, 관리하며 보안 그룹은 가장 중요한 네트워크 보안 격리 수단입니다.
– **로그인 방식**：보안성이 높은 [SSH 키 쌍](http://intl.cloud.tencent.com/document/product/213/6092)과 일반 비밀번호를 사용하는 [로그인 비밀번호](http://intl.cloud.tencent.com/document/product/213/6093)를 참조하세요.
- **리전과 가용 영역**: 인스턴스와 기타 리소스를 실행하는 위치입니다.
- **Tencent Cloud 콘솔**: 웹 기반의 사용자 인터페이스입니다.


## 클라우드 가상 머신을 사용하는 방법 

클라우드 가상 머신을 설정, 관리하기 위해 Tencent Cloud는 다음과 같은 방법을 제공합니다.

- **콘솔**: Tencent Cloud가 제공하는 웹기반의 인터페이스입니다. 클라우드 가상 머신을 설정하고 관리합니다.
- **API**：클라우드 가상 머신을 원활히 관리하기 위해, Tencent Cloud는 API 인터페이스를 제공합니다. API에 대한 자세한 사항은 [API 소개](https://intl.cloud.tencent.com/document/product/213/15688)를 참조하세요.
- **SDK**: [SDK 프로그래밍](https://intl.cloud.tencent.com/document/product/494) 혹은 Tencent Cloud [커맨드 라인 CLI](https://intl.cloud.tencent.com/document/product/1013/30220) 툴로 CVM API를 호출합니다.

##  CVM을 빠르게 구매하고 설정합니다.

개인 사용자가 처음 CVM을 구매할 경우, Tencent Cloud가 제공하는 매뉴얼을 참조하여 솔루션 설정을 추천합니다. 참고 항목:
- [윈도스 CVM 매뉴얼](http://intl.cloud.tencent.com/document/product/213/2764)
- [리눅스 CVM 매뉴얼](http://intl.cloud.tencent.com/document/product/213/2936)

스토리지 미디어, 용량, 네트워크 대역폭 및 보안 그룹 설정에 사용자 지정 등 CVM의 높은 사양을 원하시면, 다음 항목을 참조하세요.
- [윈도스 CVM 사용자 정의 설정](http://intl.cloud.tencent.com/document/product/213/10516)
- [리눅스 CVM 사용자 정의 설정](http://intl.cloud.tencent.com/document/product/213/10517)

## CVM 가격

CVM 가격은 [CVM Pricing (Linux)](https://intl.cloud.tencent.com/document/product/213/30011)를 참조하세요.

## 기타 관련 제품
 
- 오토 스케일링을 사용하여 주기적 혹은 조건에 따라 스스로 서버 클러스터 수량을 추가하거나 줄일 수 있습니다. 자세한 내용은 [오토 스케일링 제품 문서](https://intl.cloud.tencent.com/document/product/377)를 참조하세요.
- Cloud load balancer을 사용하여 멀티 CVM 인스턴스를 통합하고, 스스로 클라이언트가 보낸 쿼리 트래픽을 배분할 수 있습니다. 자세한 내용은 [Cloud load balancer 제품 문서](https://intl.cloud.tencent.com/document/product/214)를 참조하세요.
- 컨테이너 서비스를 사용하여 CVM의 애플리케이션 라이플사이클을 관리할 수 있습니다. 자세한 내용은 [컨테이너 서비스 제품 문서](https://intl.cloud.tencent.com/document/product/457)를 참조하세요.
- 클라우드 모니터링 서비스로 CVM 인스턴스 및 시스템 디스크를 모니터링할 수 있습니다. 자세한 내용은 [클라우드 모니터링 제품 문서](https://intl.cloud.tencent.com/document/product/248)를 참조하세요.
- 클라우드에 관계형 데이터 베이스를 배포하거나, Tencent Cloud 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [클라우드 데이터베이스 MySQL](https://intl.cloud.tencent.com/document/product/236)를 참조하세요.
