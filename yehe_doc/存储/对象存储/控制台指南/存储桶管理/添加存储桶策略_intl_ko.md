## 소개

COS 콘솔에서 버킷 정책을 추가하여 특정 계정, 특정 출처 IP(또는 IP 서브넷)가 정책에서 설정한 COS 리소스에 액세스하는 것을 허용 또는 거부할 수 있습니다. 버킷 정책 개요 및 정책 예시에 관한 정보는 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)와 [버킷 정책 예시](https://intl.cloud.tencent.com/document/product/436/18031)를 참조하십시오. 버킷 정책을 추가하는 자세한 방법은 다음과 같습니다.

>루트 계정당 생성할 수 있는 버킷 ACL 규칙은 최대 1000개입니다.

## 전제 조건
버킷을 생성한 상태여야 합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.

## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 [버킷 리스트]를 클릭한 뒤 버킷 정책을 추가할 버킷을 선택하여 이동합니다.
![](https://main.qcloudimg.com/raw/156823c7ad23708feb85f5d682c61d50.png)
3. [권한 관리]를 클릭한 뒤 **Policy 권한 설정**을 찾습니다. COS에서 제공하는 버킷 정책 추가 방법은 **그래픽 설정**과 **정책 구문**이 있으며, 둘 중 하나의 방법을 선택하여 버킷 정책을 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/3e3c1c923384785190720b8505e94025.png)
 - **그래픽 설정**
 설정 예시는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/950c03ba2eb714c102b68b57d025792d.png)
 - **정책 구문**
 [편집]을 클릭하여 정의한 정책 구문을 입력합니다. COS는 다양한 시나리오를 위한 정책 구문을 제공하고 있습니다. 자세한 내용은 [버킷 정책 예시](https://intl.cloud.tencent.com/document/product/436/18031)를 참조하십시오.
  ![](https://main.qcloudimg.com/raw/f449e55582e5855943c54208030a8b28.png)
4. 설정한 정보에 이상이 없으면 [확인] 또는 [저장]을 클릭합니다. 이때 서브 계정으로 COS 콘솔에 로그인하면 정책에서 정한 리소스에 한해 액세스할 수 있습니다.

