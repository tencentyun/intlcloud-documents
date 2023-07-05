## 작업 시나리오

Tencent Cloud의 네트워크는 기본 네트워크와 VPC(VPC)로 나누어지며 사용자들에게 각기 다른 양질의 서비스를 제공하고 있습니다. 이를 기반으로 편리한 네트워크 관리를 위해 아래와 같이 더욱 효율적인 서비스를 제공합니다.
- 네트워크 변경
 - **기본 네트워크를 VPC로 변경**: Tencent Cloud는 단일 CVM과 다중 CVM의 기본 네트워크를 VPC(VPC)로 변경할 수 있는 서비스를 제공합니다.
 - **VPC A를 VPC B로 변경**: Tencent Cloud는 단일 CVM과 다중 CVM의 VPC A를 VPC B로 변경할 수 있는 서비스를 제공합니다.
- 사용자 정의 IP 설정
- 기존 내부 IP 및 HostName 유지를 선택합니다.

## 전제 조건
마이그레이션하기 전에 사설망 및 공중망의 CLB 및 모든 보조 ENI에서 CVM 인스턴스를 바인딩 해제하고 기본 ENI의 보조 IP 주소를 해제합니다. 마이그레이션 후 다시 바인딩 하십시오.


## 작업 단계
### 인스턴스 네트워크 속성 확인
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. ‘인스턴스’ 리스트 탭에서 실제 뷰 모드에 따라 네트워크를 변경할 대상 인스턴스를 조회합니다.
<dx-tabs>
::: 리스트 뷰
아래 이미지와 같이 '인스턴스 설정'에서 네트워크가 '기본 네트워크'로 표시된다면 해당 인스턴스의 네트워크가 기본 네트워크임을 의미합니다.
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
:::
::: 탭 뷰
‘기본 정보’의 ‘네트워크 정보’에 네트워크가 ‘기본 네트워크’로 표시되면 인스턴스가 속한 네트워크가 기본 네트워크임을 의미합니다.
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
- 기본 네트워크를 VPC로 변경한 후에는 다시 되돌릴 수 없으며, CVM을 VPC로 변경한 후에는 다른 기본 네트워크의 클라우드 서비스와 통신할 수 없습니다.
- 기본 네트워크에서 VPC 변경 이전에 마이그레이션할 기본 네트워크의 CVM과 리전 내 VPC를 생성하고 동일한 가용존에 서브넷을 생성해야 합니다. 자세한 내용은 [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805)를 참고하십시오.
- 인스턴스의 네트워크 속성을 확인한 후, 필요에 따라 [VPC 변경](#changeVPC) 순서를 참고하여 작업하시길 바랍니다.
</dx-alert>





### VPC 변경[](id:changeVPC)
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. '인스턴스 리스트' 페이지에서 객체 인스턴스의 VPC를 변경합니다.
<dx-tabs>
::: 리스트 뷰
 - **단일 인스턴스 VPC 변경**
네트워크 변경 대상 인스턴스를 선택하고 오른쪽 작업 열에서 아래와 같이 **더 보기** > **리소스 변경** > **VPC 변경**을 선택합니다.
![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
 - **배치 인스턴스 VPC 변경**
배치 인스턴스를 VPC 변경하려면, 변경할 인스턴스를 선택하고 인스턴스 리스트 상단에서 아래와 같이 **더 많은 작업** > **리소스 변경** > **VPC 변경**을 선택합니다.
<dx-alert infotype="notice" title="">
CVM 네트워크 유형 일괄 변경 시에는 선택한 CVM 모두 반드시 동일한 가용존에 있어야 합니다.
</dx-alert> <img src="https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png"/>

:::
::: 탭 뷰
네트워크를 변경할 대상 인스턴스 탭을 선택하고 오른쪽 상단에서 아래와 같이 **더 많은 작업** > **리소스 변경** > **VPC 변경**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/8bc05f6667b7fe673bd19d77f9e26082.png)
:::
</dx-tabs>

3. 팝업된 'VPC 변경' 창에서 주의사항을 확인하고 **다음 단계**를 클릭합니다.
4. VPC 및 해당 서브넷을 선택한 뒤 **다음 단계**를 클릭합니다.
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. 필요에 따라 IP 설정에 대해 내부 IP 주소와 HostName 옵션을 다음 이미지와 같이 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5a95f5ddfc02b56ec59bba7870ea9d78.png)
주요 매개변수는 다음과 같습니다.
  - **미리 할당된 IP 주소**: 인스턴스의 기존 내부 IP를 유지하지 않는 경우 ‘미리 할당된 IP 주소’를 입력할 수 있습니다. 입력하지 않으면 시스템이 자동으로 IP 주소를 할당합니다.
  - **기존 내부 IP 유지 여부**: 필요에 따라 인스턴스의 기존 내부 IP 주소 유지 여부를 선택할 수 있습니다.
  - **HostName 옵션**: 필요에 따라 인스턴스의 기존 HostName 유지 여부를 선택할 수 있습니다. 
6. **다음 단계**를 클릭하여 CVM 종료 페이지의 지침에 따라 작업을 수행한 다음 **마이그레이션 시작**을 클릭합니다. 마이그레이션이 완료되면 CVM 콘솔에 로그인할 수 있습니다. 인스턴스 페이지에서 마이그레이션된 인스턴스의 상태 열에 **인스턴스 vpc 속성 수정**이 표시되는 것을 볼 수 있습니다.
<dx-alert infotype="notice" title="">
- 마이그레이션 과정 중 호스트 인스턴스를 재시작해야 하므로 다른 작업은 진행하지 마시길 바랍니다.
- 마이그레이션 후 인스턴스의 실행 상태, 사설망 액세스 및 원격 로그인이 정상적인지 확인합니다.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png"/>



