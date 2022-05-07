## 작업 시나리오
본 문에서는 IPv6 CIDR을 사용하여 CVM을 구축하고 ENI 카드에 IPv6을 활성화하여 IPv6 내부 및 외부 네트워크 통신을 구현하는 방법을 안내합니다.


<dx-alert infotype="explain" title="">
탄력적 공용 네트워크 IPv6, IPv6 CLB 및 IPv6 VPC 활성화 지원 리전: 광저우, 선전 파이낸스, 상하이, 상하이 파이낸스, 난징, 베이징, 청두, 홍콩, 싱가포르, 버지니아. 이용을 원하시면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)하여 신청하십시오.
</dx-alert>




## 작업 유의사항

1. Tencent Cloud 제품을 사용하기 전에 [Tencent Cloud 계정을 생성](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fconsole.intl.cloud.tencent.com%2Fworkorder%2Fcategory)해야 합니다.
2. 현재 탄력적 공용 네트워크 IPv6, IPv6 CLB 및 IPv6 VPC 활성화 지원 리전:
광저우, 선전 파이낸스, 상하이, 상하이 파이낸스, 난징, 베이징, 청두, 홍콩, 싱가포르, 버지니아. 사용을 위해서는 이용을 원하시면 [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)하여 신청하십시오.
3. IPv6 주소는 GUA 주소이며, 각 VPC에는 '/56'의 IPv6 CIDR이 할당되고, 각 서브넷에는 '/64'의 IPv6 CIDR이 할당되며, 각 ENI에는 IPv6 주소가 할당됩니다.
4. 주 ENI와 보조 ENI 모두 IPv6 주소 신청을 지원합니다. CVM과 ENI 간의 관계에 대해 자세히 알아보려면 [ENI](https://intl.cloud.tencent.com/zh/document/product/576) 제품 문서를 참고하십시오.
5. CPM 2.0은 인스턴스 생성 시 IPv6 주소 설정을 지원하지 않습니다. CPM 2.0에서 이 기능을 설정하려면 CPM 2.0 인스턴스를 생성한 후 ENI의 IPv6 콘솔로 이동하여 활성화합니다.
## 작업 단계


<dx-alert infotype="explain" title="">
IPv6은 베타 테스트 중이므로 CVM 인스턴스는 기본적으로 IPv6 주소로 설정되지 않습니다. CVM에서 IPv6 기능을 활성화해야 하는 경우 먼저 수동으로 설정하십시오.
</dx-alert>



### 1단계: CVM 구매(옵션)



<dx-alert infotype="explain" title="">
이미 CVM을 구매했다면 이 단계를 건너뛸 수 있습니다.
</dx-alert>


1. [Tencent Cloud 구매 페이지](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.87370846.770173325.1571651505)에 로그인하십시오.
2. 모델 선택 시 IPv6을 지원하는 리전과 네트워크를 선택합니다.
3. 호스트 설정 시 IPv6을 지원하는 보안 그룹을 선택하고 **무료 IPv6 주소 할당**을 선택합니다.
<dx-alert infotype="notice" title="">
선택한 네트워크 또는 보안 그룹이 IPv6을 지원하지 않는 경우 빠른 IPv6 VPC 구축을 참고하여 필요에 맞는 VPC 및 보안 그룹을 생성하십시오.
</dx-alert>
4. 구매할 CVM 정보를 확인하고 결제를 완료하십시오.

