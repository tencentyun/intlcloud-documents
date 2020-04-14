## 작업 시나리오

Tencent Cloud 상의 네트워크는 기본 네트워크와 VPC(Virtual Private Cloud)로 나뉘며 양자는 사용자에게 서로 다른 양질의 서비스를 제공하고 있습니다. 이를 기반으로 당사는 보다 유연한 서비스를 제공하여 사용자의 네트워크 관리에 편의를 주고 있습니다.
- 네트워크 간 전환
 - 기본 네트워크에서 VPC로 전환: Tencent Cloud는 단일 CVM(Cloud Virtual Machine)과 대량 CVM의 기본 네트워크에서 VPC로 전환하는 서비스를 제공합니다
 - VPC A에서 VPC B로 전환: Tencent Cloud는 단일 CVM과 대량 CVM의 VPC A에서 VPC B로 전환하는 서비스를 제공합니다
- 사용자 정의 IP 설정
- HostName 보류 기능 자주 선택

## 주의사항

- 대량 CVM의 네트워크 유형을 전환할 때 선택한 CVM은 반드시 동일한 가용존에 있어야 합니다.
- 마이그레이션 전, 내부/외부 네트워크 CLB 및 ENI를 자체로 바인딩 해제하고 주 ENI의 보조 IP를 반환하며 마이그레이션 후 다시 바인딩합니다.
- 마이그레이션 과정에서 호스트 인스턴스는 재시작해야 하며 기타 작업은 실행하지 마십시오.
- 마이그레이션 후 인스턴스 실행 상태, 내부 네트워크 액세스 및 원격 로그인 정상 여부를 점검해 주세요.
- 기본 네트워크를 VPC로 전환한 후 거꾸로 돌릴 수 없으며 CVM은 VPC로 전환한 후 기타 기본 네트워크의 CVM과 통신할 수 없습니다.

## 작업 순서

1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. "Instance" 페이지에서 네트워크 전환 예정인 인스턴스 줄을 선택하고 오른쪽 "작업"창의 [More]>[Resource Adjustment]을 클릭하여 [**Switch VPC**]을 선택합니다.
>? 대량 전환이 필요하면 네트워크 전환 예정인 인스턴스를 선택 체크하고 페이지 상단의 [More actions]>[Resource Adjustment]을 클릭하여 [**Switch VPC**]을 선택할 수 있습니다.
3. 팝업된 "Switch VPC" 창에서 주의사항을 확인하고 [Next]를 클릭합니다.
4. VPC 및 상응하는 서브넷을 선택하고 [Next]를 클릭합니다.
5. 실제 수요에 근거해 선택한 서브넷에서 할당 예정인 IP 주소를 설정하고 HostName 옵션을 선택한 후 [Next]를 클릭합니다.
>? 
> - "할당 예정 IP 주소"를 작성하지 않으면 시스템은 자동으로 할당합니다.
> - HostName 옵션을 설정할 때 사용자는 VPC 전환과 동시에 인스턴스 HostName 재설정을 선택하거나 인스턴스 기존 HostName 보류를 선택할 수 있습니다.
> 
6. 종료 제시어에 따라 작업을 실행하고 [Start Migration]을 클릭하면 바로 콘솔 페이지에서 인스턴스 상태를 "인스턴스 vpc 속성 수정"으로 수정할 수 있습니다. 아래 그림 참조
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)
