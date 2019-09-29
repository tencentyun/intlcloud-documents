### BGP ASN
BGP 라우팅에 사용되는 모든 자치 시스템에 유일한 번호가 할당됩니다. 자치 시스템 번호(ASN)는 인터넷 할당 번호 관리 기관(Internet Assigned Numbers Authority, IANA, 이 기관은 인터넷 IP 주소도 할당함)에 의해 각 지역 인터넷 등록 관리 기관(RIR)에 배치로 할당됩니다. 각 지역의 RIR은 IANA로부터 할당한 전체 ASN에서 하나의 실체에 ASN 하나를 할당합니다. ASN을 요구하는 실체는 속한 지역 센터가 규정한 프로세스에 따라 신청해야 하며, 승인을 받은 후 ASN 하나를 할당하게 됩니다.


### 피어링 연결
<a href="https://cloud.tencent.com/doc/product/215/5000" target="_blank">피어링 연결</a>(peering connection)은 다른 VPC가 생성한 연결로 계정 간과 지역 간의 VPC 트래픽 상호 연결을 지원합니다.

### IPsec
IPsec(Internet Protocol Security)은 인터넷 보안 프로토콜이라고도 합니다. 프로토콜 패킷으로 IP 프로토콜 그룹에 대한 암호화와 인증을 통해 IP 프로토콜의 네트워크 전송 프로토콜 패밀리(상호 연결한 프로토콜의 집함)를 보호할 수 있습니다.
IPsec은 일반적으로 다음 프로토콜로 구성됩니다.
- **인증 헤더**: IP 데이터 메시지에 데이터 무결성, 메시지 인증을 제공하고 및 재전송 공격을 방어합니다.
- **캡슐화된 보안 부하**: 기밀성, 데이터 소스 인증, 무결성, 재전송 공격 방어 및 제한적 흐름 기밀성을 제공합니다.
- **보안 연결**: 알고리즘과 데이터 패킷을 제공하며, 인증 헤더, 캡슐화된 보안 부하 작업에 필요한 매개변수도 제공합니다.


### 라우팅 테이블
<a href="https://cloud.tencent.com/doc/product/215/4954" target="_blank">라우팅 테이블</a>(Routing Table)은 일련의 라우팅 전략을 포함하며 VPC 내 모든 서브넷의 네트워크 트래픽 경향을 정의하는 데 사용됩니다. 서브넷마다 단 하나의 연결 라우팅 테이블이 있으며, 모든 라우팅 테이블은 동일 VPC 중 여러 개의 서브넷을 연결할 수 있습니다.

### VPC
VPC(Virtual Private Cloud)는 Tencent Cloud에 독립적인 네트워크 공간을 구축하며, 데이터 센터에서 실행한 전통 네트워크와 매우 유사합니다. 하지만 VPC는 Tencent Cloud에서 <a href="https://cloud.tencent.com/doc/product/213/495" target="_blank">CVM</a>, <a href="https://cloud.tencent.com/doc/product/214/524" target="_blank">CLB</a>, <a href="https://cloud.tencent.com/document/product/236" target="_blank">Cloud Database</a> 등 클라우드 서비스 리소스를 호스팅합니다. 네트워크 장치 구매와 OPS를 전혀 적정할 필요 없이 소프트웨어를 통해 IP 주소 범위, IP 주소, 라우팅 전략 등을 사용자 지정할 수 있습니다. <a href="https://cloud.tencent.com/doc/product/213/1941" target="_blank">EIP</a>, <a href="https://cloud.tencent.com/doc/product/215/4975" target="_blank">NAT 게이트웨이</a> 및 <a href="https://cloud.tencent.com/doc/product/215/4972" target="_blank">공중망 게이트웨이</a> 등을 통해 유연하게 Internet에 접근할 수 있습니다. 그 동시에 <a href="https://cloud.tencent.com/doc/product/215/4956" target="_blank"> VPN</a>/<a href="https://cloud.tencent.com/doc/product/215/4976" target="_blank">DC</a>로 VPC와 귀하의 데이터 센터를 연결시켜 VPC의 <a href="https://cloud.tencent.com/doc/product/215/5000" target="_blank">피어링 연결</a> 서비스는 전세계 동일 서버와 2-지역-3 DC 재해 복구를 구현할 수 있도록 도와드립니다. 그 밖에, VPC의 <a href="https://cloud.tencent.com/doc/product/213/500" target="_blank">보안 그룹</a>과 <a href="https://cloud.tencent.com/doc/product/215/5132" target="_blank">네트워크 ACL</a>은 전면적으로 귀하의 네트워크 보안 요구를 만족시킵니다.

### VLAN ID
VLAN(Virtual Local Area Network), 가상 랜이라고도 하며 랜 교환 기술에 기초로 네트워크 관리 기술입니다. 교환기는 일반적으로 255개 VLAN으로 나뉘며, 각 VLAN ID는 1 - 4096 중 임의 숫자가 가능합니다. ID는 VLAN을 구분하는 데 사용되며, TAG UNTag member 속성을 설정할 수 있고 해당 포트의 다운스트림/업트림 데이터 메시지에 라벨을 붙일 수도 있습니다.


### 물리적 직접 연결
물리적 직접 연결은 Tencent Cloud와 로컬 IDC를 연결한 물리적 회선으로, 물리적 직접 연결 1개는 여러 지역의 직접 연결 게이트웨이와 직접 연결 터널을 생성할 수 있습니다.

### 서브넷
<a href="https://cloud.tencent.com/doc/product/215/4927" target="_blank">서브넷</a>(Subnet)은 VPC IP 주소 범위를 유연하게 구획합니다. 사용자는 다른 서브넷에 응용 프로그램과 서비스를 배포할 수 있어 안전하고 유연하게 Tencent Cloud VPC에서 멀티 웹 응용 프로그램을 호스팅할 수 있습니다.

### Direct Connect
<a href="https://cloud.tencent.com/doc/product/215/4976" target="_blank">DC</a>(Direct Connect)는 Tencent Cloud와 로컬 IDC를 빠르게 연결하는 방법으로, 물리적 직접 연결을 통해 여러 지역에 위치한 Tencent Cloud 컴퓨팅 리소스를 한 번에 연결할 수 있고 유연하고 믿을 만한 하이브리드 클라우드 구축을 구현할 수 있습니다. DC는 단일 장애점이 없는 듀얼 라인 핫 백업 액세스 방식을 지원하여 금융 등 네트워크 상호 연결 요구를 만족시킵니다.

### 전용 채널
전용 채널은 물리적 직접 연결의 네트워크 링키지 구획으로 다른 직접 연결 게이트웨이에 연결한 전용 채널을 생성하여 로컬 IDC와 여러 VPC의 상호 연결을 구현할 수 있습니다.

### 직접 연결 게이트웨이
직접 연결 게이트웨이는 VPC의 직접 연결 트래픽 입구로 여러 전용 채널과 여러 로컬 IDC를 상호 연결할 수 있습니다.
