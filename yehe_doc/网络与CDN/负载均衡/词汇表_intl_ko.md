## A

### 보안 그룹

보안 그룹(Security Group)은 패킷을 필터링할 수 있는 스테이트풀 가상 방화벽입니다. 하나 이상의 CVM 인스턴스에 대한 네트워크 액세스 제어를 설정하는 데 사용할 수 있습니다. 한 리전에서 동일한 네트워크 보안 격리 요구가 있는 인스턴스를 동일한 보안 그룹에 넣을 수 있으며, 해당 그룹의 네트워크 정책을 통해 아웃바운드 및 인바운드 트래픽을 필터링할 수 있습니다.

## C

### CLB

자세한 내용은 [Cloud Load Balancer(CLB)](#clb)를 참고하십시오.

## D

### 리전

리전(Region)은 Tencent Cloud 관리형 데이터 센터가 있는 곳입니다. 한 리전에 서로 다른 가용존(AZ)이 있을 수 있습니다.
예를 들어 베이징은 관리형 데이터 센터가 있는 리전이고 AZ는 베이징 1존 입니다. 같은 리전의 Tencent Cloud 서비스는 사설망을 통해 서로 통신할 수 있지만 다른 리전의 서비스는 그렇지 않습니다. 액세스 지연을 최소화하고 다운로드 속도를 향상시키기 위해 최종 사용자와 가장 가까운 리전을 선택하는 것이 좋습니다.

## F
<span id="clb"></span>
### CLB

Cloud Load Balancer(CLB)는 Tencent Cloud에서 제공하는 안전하고 안정적이며 탄력적으로 확장 가능한 트래픽 분산 서비스입니다. 단일 실패 지점을 방지하여 시스템 가용성을 향상시킵니다.

### CLB 리스너

CLB(CloudLoadBalancer) 리스너는 요청 분배 규칙을 제공하며 수신 포트, 로드 밸런싱 정책 및 상태 확인 구성이 포함됩니다. 요청은 리스너 구성에 따라 리얼 서버로 전달됩니다. CLB 인스턴스에는 하나 이상의 리스너가 있어야 합니다.

### CLB 인스턴스

CLB 인스턴스(CloudLoadBalancer Instance)는 실행 중인 CLB 서비스입니다. CLB를 사용하려면 먼저 CLB 인스턴스를 생성해야 합니다.

## H
<span id="RS"></span>
### 리얼 서버

리얼 서버(Real Server, RS)는 CLB에서 배포한 요청을 처리하는 데 사용되는 CVM 인스턴스 세트입니다.

## R

### RS

자세한 내용은 [리얼 서버](#RS)를 참고하십시오.

## S
<span id="vpc"></span>
### VPC

VPC(Virtual Private Cloud)는 Tencent Cloud에 별도의 네트워크 공간을 구축합니다. 이는 VPC에서 호스팅되는 서비스가 [CVM](https://intl.cloud.tencent.com/document/product/213), [CLB](https://intl.cloud.tencent.com/document/product/214) 및 [TencentDB](https://intl.cloud.tencent.com/document/product/236)와 같은 Tencent Cloud 서비스의 리소스라는 점을 제외하고 IDC에서 실행되는 기존 네트워크와 매우 유사합니다. 네트워크 장치의 조달 및 OPS에 대해 전혀 걱정할 필요가 없습니다. 대신 사용하기 쉬운 소프트웨어 프로그램을 통해 IP 범위, IP 주소, 라우팅 정책 등을 사용자 지정하기만 하면 됩니다. [EIP](https://intl.cloud.tencent.com/document/product/213/16586), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) 및 [공용 게이트웨이](https://intl.cloud.tencent.com/document/product/213/34835)를 사용하여 인터넷에 유연하게 액세스하거나 [VPN](https://intl.cloud.tencent.com/document/product/215) / [Direct Connect](https://intl.cloud.tencent.com/document/product/216)를 통해 IDC와 VPC를 상호 연결할 수 있습니다. 또한, VPC의 [Peering Connection](https://intl.cloud.tencent.com/document/product/553) 서비스는 글로벌 액세스 및 2리전 3데이터센터 재해 복구를 위한 통합 서버를 쉽게 구현할 수 있도록 도와주며 VPC의 보안 그룹 및 [Network ACL](https://intl.cloud.tencent.com/document/product/215/31850) 기능은 다차원적이고 포괄적인 방식으로 네트워크 보안 요구를 충족시킬 수 있습니다.

## V

### VIP

자세한 내용은 [VIP](#vip)를 참고하십시오.

### VPC

자세한 내용은 [VPC](#vpc)를 참고하십시오.

## X
<span id="vip"></span>
### VIP

버츄얼 IP(virtual IP, VIP)는 시스템에서 CLB 인스턴스에 할당한 IP 주소입니다. 사설망 또는 공중망 CLB 인스턴스를 생성하기 위해 인터넷에 공개할지 여부를 선택할 수 있습니다. 도메인 이름을 공개 VIP에 레졸루션하여 서비스를 제공할 수 있습니다.