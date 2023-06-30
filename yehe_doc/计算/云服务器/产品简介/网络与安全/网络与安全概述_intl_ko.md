Tencent Cloud는 네트워크와 보안 그룹을 제공하여 사용자의 인스턴스 보안, 효율, 자유로운 대내외적 서비스 제공을 보장합니다.

## 암호화 로그인 방식
Tencent Cloud는 [로그인 비밀번호](https://intl.cloud.tencent.com/document/product/213/6093)와 [SSH 키 ](https://intl.cloud.tencent.com/document/product/213/6092)의 두 가지 암호화된 로그인 방식을 제공합니다. 사용자는 자유롭게 로그인 방식을 선택하여 안전하게 CVM 연결을 진행할 수 있습니다. Windows 시스템 인스턴스는 SSH 키 로그인이 지원되지 않습니다.

## 네트워크 액세스
Tencent Cloud에 있는 클라우드 서비스는 [공용망 서비스](https://intl.cloud.tencent.com/document/product/213/5224) 또는 [인트라넷 서비스](https://intl.cloud.tencent.com/document/product/213/5225)를 통해 액세스할 수 있습니다.
 - Internet 액세스: Internet 액세스는 Tencent Cloud에서 인스턴스에 제공하는 공개 데이터 전송 서비스입니다. 인스턴스는 공용 네트워크 상의 다른 컴퓨터와 통신할 수 있도록 공용 IP 주소가 할당됩니다.
 - 내부 네트워크 액세스: 내부 네트워크, 즉 LAN 서비스는 Tencent Cloud가 인스턴스에 개인 IP 주소를 제공하여 구현하는 동일 리전 내 무상 내부 네트워크 통신 서비스입니다.

## 네트워크 환경
Tencent Cloud의 [네트워크 환경](https://intl.cloud.tencent.com/document/product/213/5227)은 기본 네트워크와 VPC로 나눌 수 있습니다.
 - 기본 네트워크: 기본 네트워크는 Tencent Cloud 상의 모든 사용자의 공용 네트워크 리소스 풀입니다. Tencent Cloud를 이제 막 사용하기 시작한 사용자에게 적합합니다.
 - VPC: VPC는 로직이 격리된 사용자 정의 네트워크 공간입니다. 사전 설정되고 사용자 정의된 IP 범위에서 CVM 인스턴스를 실행하여 다른 사용자로부터 리소스를 격리할 수 있습니다. 네트워크 관리에 익숙한 사용자에게 적합합니다.

## 보안 그룹
[보안 그룹](https://intl.cloud.tencent.com/document/product/213/12452)은 필터링 기능이 포함된 스테이트풀 가상 방화벽의 일종으로, 단일 또는 다중 CVM 에 대한 네트워크 액세스 제어 설정에 사용됩니다. Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 수단입니다.
다음과 같은 방법으로 인스턴스의 액세스 권한을 통제할 수 있습니다.
 - 다중 보안 그룹을 생성하여 보안 그룹마다 다른 규칙을 지정합니다.
 - 각각의 인스턴스에 하나 또는 여러 개의 보안 그룹을 연결합니다. Tencent Cloud는 이러한 보안 그룹을 사용하여 인스턴스에 대한 트래픽 액세스와 인스턴스가 액세스할 수 있는 리소스를 제어합니다. 
 - 보안 그룹 생성은 특정 IP 주소 또는 특정 보안 그룹만을 인스턴스에 액세스할 수 있게 합니다.

## EIP
[EIP](https://intl.cloud.tencent.com/document/product/213/5733)(Elastic IP, 약칭: EIP)는 독립적으로 구매 및 보유할 수 있으며, 특정 리전에 고정된 공용 IP 주소입니다.
다음 시나리오에서 EIP 사용을 권장합니다.
 - 인스턴스가 통제 불가한 원인으로 인해 다운될 수 있으므로, 액세스를 보장하기 위해 동일한 IP 주소의 대체 인스턴스가 필요한 경우.
 - 인스턴스에 공용 IP 주소가 없어, 정적 IP 주소가 필요한 경우.

## ENI
[ENI](https://intl.cloud.tencent.com/document/product/213/6514)(Elastic Network Interface)는 VPC 내의 CVM을 바인딩하는 일종의 탄력적 네트워크 인터페이스로서, 여러 CVM 간에 자유롭게 마이그레이션할 수 있습니다. ENI는 관리 네트워크 설정 및 신뢰도 높은 네트워크 솔루션의 구축에 큰 도움이 됩니다.

## CWP
Cloud Workload Protection(CWP)은 Tencent Security가 축적한 방대한 보안 리스크 데이터를 기반으로, 머신 러닝을 통해 사용자에게 제공하는 해커 침입 감지, 취약점 리스크 알람 등 보안 서비스입니다. 주로 비밀번호 크래킹 차단, 원격 로그인 알림, 트로이 목마 파일 감지, 고위험 취약점 모니터링 등 다양한 기능을 포함하고 있습니다. 서버가 직면한 네트워크 보안 리스크를 해결하고, 기업의 서버 보안 체계 구축을 지원하여, 데이터 유출을 방지합니다.

## Anti-DDoS Basic
Anti-DDoS Basic은 Tencent Cloud에서 CVM, CLB 등 리소스에 무상 제공하는 기본 DDoS 보호 기능으로, 일상적인 보안 운영 요구 사항을 충족합니다. Tencent Cloud는 사용자의 보안 상태에 따라 차단 처리 임계값을 동적 조정합니다. Anti-DDoS Basic은 기본적으로 활성화되어 있으며, 실시간으로 네트워크 트래픽을 모니터링하고, 공격 발견 즉시 클리닝을 실시하여, 단 몇 초안에 Tencent Cloud 공용 IP에 대한 보호를 구현합니다.
