## 작업 시나리오
Tencent Cloud는 필요에 따라 공용 네트워크 과금 방식 또는 공용 네트워크 대역폭 변경을 지원하며, 변경 즉시 적용됩니다. 대역폭 변경과 과금 방식 제한 및 변경 후의 요금 설명은 [공용 네트워크 과금 변경](https://intl.cloud.tencent.com/document/product/213/10580)을 참조하십시오.

## 작업 순서
#### 과금 방식 변경
Tencent Cloud는 **트래픽 과금**과 **대역폭 과금**의 두 가지 유형의 과금 방식을 제공합니다. 콘솔에서 네트워크 과금 방식을 변경할 수 있습니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 ‘인스턴스’ 페이지 상단에서 대역폭을 변경할 CVM 인스턴스의 소재 리전을 선택합니다.
2. 타깃 CVM 인스턴스가 있는 행의 오른쪽에서 [더보기]>[리소스 변경]>[네트워크 변경]을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/b7b347e13cbcfe55224d7132c77be5a2.png)
3. 출력된 '네트워크 변경' 대화 상자에서 변경할 타깃 과금 방식을 선택하고 [확인]을 클릭합니다.

#### 공용 네트워크 대역폭 변경
Tencent Cloud는 **독점형 공용 네트워크**와 **공유형 공용 네트워크**의 두 가지 네트워크 설정을 지원합니다. 그 중, 공유형 공유 네트워크 서비스는 대역폭 패키지에 따라 과금하는 방식으로 현재 베타 테스트 중입니다. 사용을 원하시면 [베타 신청](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8)을 제출해 주십시오. 본 문서에서는 주로 독점형 공용 네트워크 설정 변경 방법, 즉 단일 CVM의 과금 방식에서 대역폭 최댓값을 변경하는 방법을 소개합니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인한 뒤 ‘인스턴스’ 페이지 상단에서 대역폭을 변경할 CVM 인스턴스의 소재 리전을 선택합니다.
3. 타깃 CVM 인스턴스가 있는 행의 오른쪽에서 [더보기]>[리소스 변경]>[네트워크 변경]을 선택합니다. 다음 이미지를 참고하십시오.
![](https://main.qcloudimg.com/raw/b7b347e13cbcfe55224d7132c77be5a2.png)
4. 출력된 'Adjust Network' 대화 상자에서 타깃 대역폭 값을 설정하고 [확인]을 클릭합니다.
>?대역폭 최댓값은 [공용 네트워크 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)을 참조하십시오.


## 관련 문서

- [공용 네트워크 과금 변경](https://intl.cloud.tencent.com/document/product/213/10580)
- [공용 네트워크 과금 방식](https://intl.cloud.tencent.com/document/product/213/10578) 
- [BWP 과금 방식](https://intl.cloud.tencent.com/document/product/684/15255)
- [공용 네트워크 대역폭 최댓값](https://intl.cloud.tencent.com/document/product/213/12523)
