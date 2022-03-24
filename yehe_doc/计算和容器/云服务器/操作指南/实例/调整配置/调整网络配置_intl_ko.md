## 작업 시나리오
Tencent Cloud는 필요에 따라 공용 네트워크 과금 방식 또는 공용 네트워크 대역폭 변경을 지원하며, 변경 즉시 적용됩니다. 대역폭 변경과 과금 방식 제한 및 변경 후의 요금 설명은 [공용 네트워크 과금 변경](https://intl.cloud.tencent.com/document/product/213/10580)을 참고하십시오.

## 작업 단계
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 ‘인스턴스’ 페이지 상단에서 대역폭을 변경할 CVM 인스턴스의 소재 리전을 선택합니다.
2. 인스턴스의 관리 페이지에서 사용된 실제 뷰 모드에 따라 작업합니다.
<dx-tabs>
::: 리스트 뷰
아래 이미지와 같이 타깃 CVM 인스턴스가 있는 행의 오른쪽에서 **더보기** > **리소스 변경** > **네트워크 변경**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/bcece3bef3230a16bbe4b00e71105cf8.png)

:::
::: 탭 뷰
아래 이미지와 같이 타깃 CVM 인스턴스 페이지의 오른쪽 상단에서 **더보기** > **리소스 변경** > **네트워크 변경**을 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4a57295676734b183310cfc8f06a8e25.png)

:::
</dx-tabs>
3. '네트워크 변경' 팝업 창에서 필요에 따라 공용 네트워크 과금 방식 또는 공용 네트워크 대역폭을 변경합니다.
 - 네트워크 과금 방식[](id:adjustModule): Tencent Cloud는 **트래픽 과금**과 **대역폭 과금**의 두 가지 유형의 네트워크 과금 방식을 제공합니다. 그 중 대역폭 과금 방식은 **대역폭 시간 단위 후불** 방식이 있습니다.
 - 타깃 대역폭 최댓값[](id:adjustBandwidth): Tencent Cloud는 **전용형 공용 네트워크** 및 **공유형 공용 네트워크**의 두 가지 네트워크 설정을 제공합니다. 그 중 공유형 공용 네트워크 서비스는 대역폭 패키지에 따라 과금되며, 현재 내부 베타 중입니다. 본문은 전용형 공용 네트워크 설정 변경, 즉 단일 CVM 대역폭 변경을 예로 들어 설명합니다.
<dx-alert infotype="explain" title="">
대역폭 최댓값은 [공용 네트워크 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)을 참고하십시오.
</dx-alert>
4. 변경할 타깃 과금 방식을 선택하거나 타깃 대역폭 값을 설정하고 **확인**을 클릭합니다.



## 관련 문서

- [공용 네트워크 과금 변경](https://intl.cloud.tencent.com/document/product/213/10580)
- [공용 네트워크 과금 방식](https://intl.cloud.tencent.com/document/product/213/10578) 
- [BWP 과금 방식](https://intl.cloud.tencent.com/document/product/684/15254)
- [공용 네트워크 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)
