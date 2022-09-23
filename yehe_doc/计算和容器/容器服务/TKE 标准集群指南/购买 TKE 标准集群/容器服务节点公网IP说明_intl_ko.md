공용 네트워크에 액세스하는 동안 회사 IP가 노출되는 것을 방지하고 싶지 않다면 Tencent Cloud [NAT Gateway](https://intl.cloud.tencent.com/document/product/215/4975)를 사용할 수 있습니다. 본 문서에서는 NAT Gateway를 통해 공용 네트워크에 액세스하는 방법을 설명합니다.

## 공용 IP
클러스터가 생성되면 기본적으로 클러스터의 노드에 공용 IP가 할당됩니다. 이러한 공용 IP를 사용하여 다음을 수행할 수 있습니다.
- 클러스터의 노드에 로그인합니다.
- 공용 네트워크에서 서비스에 액세스합니다.

## 공용 네트워크 대역폭
공용 네트워크에서 서비스를 생성할 때 공용 네트워크 CLB는 노드의 대역폭과 트래픽을 사용합니다. 공용 네트워크 서비스가 필요한 경우 노드에 공용 네트워크 대역폭이 있어야 합니다. 필요하지 않은 경우 공용 네트워크 대역폭을 구매하지 않을 수도 있습니다.

## NAT Gateway
CVM 인스턴스는 EIP에 바인딩되지 않으며 Internet에 액세스하는 모든 트래픽은 NAT Gateway를 통해 포워딩됩니다. 이러한 방식으로 인스턴스의 Internet에 액세스하는 트래픽은 사설망을 통해 NAT Gateway로 포워딩됩니다. 즉, 트래픽은 인스턴스를 구매할 때 지정한 공용 네트워크 대역폭의 최댓값에 적용되지 않으며 NAT Gateway에서 생성된 트래픽은 인스턴스의 공용 네트워크 대역폭 송신을 차지하지 않습니다. NAT Gateway를 통해 Internet에 액세스하려면 다음 단계를 따르십시오.

### 1단계: NAT Gateway 생성
1. [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1)에 로그인하고 왼쪽 사이드바에서 [[NAT Gateway](https://console.cloud.tencent.com/vpc/nat?rid=1)]를 클릭합니다.
2. ‘NAT Gateway’ 관리 페이지에서 **Create**를 클릭합니다.
3. ‘Create an NAT Gateway’ 팝업 창에서 다음 매개변수를 입력합니다.
 - 게이트웨이 이름: 사용자 정의.
 - 네트워크: NAT Gateway 서비스의 VPC를 선택합니다.
 - 게이트웨이 유형: 실제 필요에 따라 선택합니다. 게이트웨이 유형은 생성 후 변경할 수 있습니다.
 - 아웃바운드 대역폭 최댓값: 실제 필요에 따라 설정합니다.
 - EIP: NAT Gateway에 EIP를 할당합니다. 기존 EIP를 선택하거나 새 EIP를 구입할 수 있습니다.
4. **Create**를 클릭하여 NAT Gateway 생성을 완료합니다.
>! NAT Gateway 생성 시 1시간의 대여료가 동결됩니다.

### 2단계: 서브넷과 연결된 라우팅 테이블 설정

>? NAT Gateway가 생성되면 VPC 콘솔의 라우팅 테이블 페이지에서 라우팅 규칙을 구성하여 서브넷 트래픽을 NAT Gateway로 리디렉션해야 합니다.
>

1. 왼쪽 사이드바에서 [[Route Table](https://console.cloud.tencent.com/vpc/route?rid=1)]을 클릭합니다.
2. 라우팅 테이블 목록에서 Internet에 액세스해야 하는 서브넷과 연결된 라우팅 테이블 ID/이름을 클릭합니다.
3. ‘Routing Policy’ 섹션에서 ** New routing policy**를 클릭합니다.
3. ‘Add routing’ 페이지에서 **Destination**을 입력하고 **Next Hop Type**에 대해 **NAT Gateway**를 선택한 후 **Next Hop**에 대해 생성된 NAT Gateway의 ID를 선택합니다.
4. **OK**를 클릭합니다.
이제 라우팅 테이블과 연결된 서브넷의 CVM 인스턴스가 Intenet에 액세스할 때 생성되는 트래픽이 NAT Gateway로 전달됩니다.

## 기타 솔루션

### 솔루션1: EIP 사용
CVM 인스턴스는 EIP에만 바인딩되지만 NAT Gateway는 사용하지 않습니다. 이 솔루션을 사용하면 Internet에 액세스하는 인스턴스의 모든 트래픽이 EIP를 통해 나가며 인스턴스 구매 시 지정한 공용 네트워크 대역폭의 최댓값이 적용됩니다. 인터넷 액세스 요금은 인스턴스 네트워크의 과금 방식에 따라 부과됩니다.
자세한 내용은 [Elastic Public IP](https://intl.cloud.tencent.com/document/product/215/4958#.E6.93.8D.E4.BD.9C.E6.8C.87.E5.8D.97)를 참고하십시오.

### 솔루션2: NAT Gateway와 EIP를 모두 사용
NAT Gateway와 EIP를 모두 사용하는 경우 Internet에 접속하는 CVM 인스턴스의 모든 트래픽은 사설망을 통해 NAT Gateway로 포워딩되고, 응답 패킷은 NAT Gateway를 통해 인스턴스로 반환됩니다. 즉, 트래픽은 인스턴스를 구매할 때 지정한 공용 네트워크 대역폭의 최댓값이 적용되지 않으며 NAT Gateway에서 생성된 트래픽은 인스턴스의 공용 네트워크 대역폭 송신을 차지하지 않습니다. Internet 트래픽이 인스턴스의 EIP에 능동적으로 접근하면 인스턴스의 응답 패킷이 모두 EIP를 통해 반환됩니다. 이 경우 아웃바운드 공용 네트워크 트래픽은 인스턴스를 구매할 때 지정된 공용 네트워크 대역폭의 최댓값이 적용됩니다. 공용 네트워크 액세스 요금은 인스턴스 네트워크의 과금 방식에 따라 부과됩니다.

>! 계정에서 대역폭 패키지(BWP) 기능이 활성화된 경우 NAT Gateway에서 생성된 아웃바운드 트래픽 요금이 BWP에서 공제됩니다(즉, 네트워크 트래픽이 0.12 USD/GB로 반복적으로 청구되지 않음). 과도한 아웃바운드 대역폭으로 인한 높은 BWP 요금을 피하기 위해 NAT Gateway의 아웃바운드 대역폭을 제한하는 것이 좋습니다.
