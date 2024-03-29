## 작업 시나리오


인스턴스가 예기치 않게 폐기되는 것을 방지하기 위해 폐기 방지를 활성화할 수 있습니다.

폐기 방지가 활성화되면 콘솔에서 또는 API를 사용하여 인스턴스를 종료할 수 없습니다. 필요에 따라 언제든지 이 설정을 비활성화할 수 있습니다.

## 관련 설명
- 인스턴스 폐기 방지는 기본적으로 비활성화되어 있습니다.
- 인스턴스 폐기 방지는 시스템 수준에서 적용되지 않습니다. 예를 들어, 종량제 인스턴스가 연체로 인해 종료되는 경우 보호가 적용되지 않습니다.


## 작업 단계

### 폐기 방지 활성화
<dx-tabs>
::: 기존 인스턴스
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index)에 로그인합니다.
2. 필요에 따라 하나 이상의 인스턴스에 대해 인스턴스 폐기 방지를 활성화할 수 있습니다.
 - **하나의 인스턴스**:
‘인스턴스’ 페이지에서 타깃 인스턴스를 찾아 **더 보기** > **인스턴스 설정** > **인스턴스 폐기 방지**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/15767ce2a7a65c8679352fbb72845596.png)
 - **여러 인스턴스**:
‘인스턴스’ 페이지에서 타깃 인스턴스를 선택하고 **더 보기** > **인스턴스 설정** > **인스턴스 폐기 방지**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0c2634e3199faed37d5fdfb68131a3ca.png)
3. ‘인스턴스 폐기 방지’ 팝업 창에서 ‘활성화’를 선택하고 **확인**을 클릭합니다.

:::
::: 새로 구매한 인스턴스

인스턴스를 구매할 때 ‘사용자 지정 구성’을 선택하고 ‘2. 전체 구성’ 탭에서 ‘인스턴스 폐기 방지’를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/610370e5d6e195a41e6d1536564dedd9.png)
<dx-alert infotype="explain" title="">
기타 매개변수에 대한 자세한 내용은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.
</dx-alert>

:::
</dx-tabs>




### 인스턴스 폐기 방지 비활성화
인스턴스가 종료될 수 있다고 확신하는 경우 아래 단계에 따라 인스턴스 폐기 방지를 비활성화하십시오.


1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/instance/index)에 로그인합니다.
2. 필요에 따라 하나 이상의 인스턴스에 대한 인스턴스 폐기 방지를 비활성화할 수 있습니다.
 - **하나의 인스턴스**:
‘인스턴스’ 페이지에서 타깃 인스턴스를 찾아 **더 보기** > **인스턴스 설정** > **인스턴스 폐기 방지**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/15767ce2a7a65c8679352fbb72845596.png)
 - **여러 인스턴스**:
‘인스턴스’ 페이지에서 타깃 인스턴스를 선택하고 **더 보기** > **인스턴스 설정** > **인스턴스 폐기 방지**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0c2634e3199faed37d5fdfb68131a3ca.png)
3. ‘인스턴스 폐기 방지’ 팝업 창에서 ‘비활성화’를 선택하고 **확인**을 클릭합니다.



## 관련 문서
- [CVM 구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)
- [인스턴스 폐기/반환](https://intl.cloud.tencent.com/document/product/213/4930)
