## 소개

EIP는 탄력적인 IP 주소 또는 탄력적인 IP라고도 합니다. 이는 동적 클라우드 컴퓨팅을 위해 설계한 맞춤형 정적 IP 주소로, 어느 한 리전에 고정된 공인 IP 주소입니다. EIP 주소를 통해 계정의 다른 인스턴스 또는 NAT Gateway 인스턴스로 빠르게 다시 매핑하여 인스턴스 장애를 차단할 수 있습니다.

EIP를 릴리스하기 전까지 계정에 보관할 수 있습니다. 공인 IP는 CVM과 같이 있어야만 릴리스를 신청할 수 있는 것에 비해, EIP는 CVM의 라이프사이클과 분리되어 클라우드 리소스로 단독 작업이 가능합니다. 예를 들어 비즈니스와 큰 관련이 있는 공인 IP를 보관해야 할 경우, 이를 EIP로 전환한 후 계정에 보관할 수 있습니다.

## 규칙과 제한

### 사용 규칙

- EIP 주소는 기본 네트워크와 VPC 인스턴스 및 VPC의 [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) 인스턴스에 동시에 적용할 수 있습니다.
- EIP 주소와 CVM 인스턴스를 바인딩할 경우, 인스턴스의 현재 공인 IP 주소가 릴리스됩니다.
- CVM/NAT 게이트웨이 인스턴스를 폐기할 경우, EIP 주소와의 연결이 차단됩니다.
- EIP의 과금 규칙과 관련된 내용은 [EIP 과금](https://intl.cloud.tencent.com/document/product/213/17156)을 참조 바랍니다.
- EIP 작업 순서와 관련된 내용은 [EIP](https://intl.cloud.tencent.com/document/product/213/16586)를 참조 바랍니다.
 
### 쿼터 제한

| 리소스 | 제한 |
|---------|:---------:|
| 각 Tencent Cloud 계정별 리전(Region)에 할당된 EIP 개수 | 20개 |
| 각 Tencent Cloud 계정별 리전의 일일 주문 횟수	 | 쿼터수 \* 2회 |
| EIP 바인딩 해제 시 계정당 일일 무료 공인 IP를 재할당 가능 횟수 | 10회 |

> EIP 할당은 조정할 수 없도록 기본 설정되어 있어 [NAT Gateway](https://intl.cloud.tencent.com/product/nat), [CLB](https://intl.cloud.tencent.com/document/product/214)를 통해 IP 컨버전스를 진행할 수 있습니다.
> - 특수한 상황으로 인해 조정이 필요할 경우, 계정에 해당하는 범위의 클라우드 서비스 리소스가 있어야 합리적으로 사용할 수 있습니다.
> - 요구되는 쿼터가 비교적 높을 경우 초과한 쿼터는 요금이 부과될 수 있습니다.
>- 조정 후에 IP를 너무 자주 교체하거나 적용 법률 법규를 위반한 경우, Tencent Cloud는 쿼터를 철회할 권리가 있습니다.
>


### CVM의 공인 IP 바인딩 제한

2019년 9월 18일(포함)부터 CPU 구성의 차이에 따라, 단일 CVM의 공인 IP 바인딩 수량 최댓값이 아래 표와 같이 변경되었습니다.
> 2019년 9월 18일 0시 전에 구매한 CVM은 이 제한을 받지 않으며 해당 CVM이 지원하는 공인 IP 바인딩 수량은 사용자의 서버가 지원하는 [개인 IP 수량](https://intl.cloud.tencent.com/document/product/576/18527)과 동일합니다.
>

| CVM의 CPU 수 | 바인딩 가능한 공인 IP 수량 최댓값(일반 공인 IP와 EIP 포함) |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



