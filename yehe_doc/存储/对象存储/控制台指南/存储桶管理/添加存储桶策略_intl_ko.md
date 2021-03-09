## 소개

COS 콘솔을 통해 버킷 정책을 추가함으로써 임의의 계정이나 출처 IP(또는 IP 필드)가 정책이 설정된 COS 리소스에 액세스하는 것을 허용 또는 금지할 수 있습니다. 버킷 정책 개요 및 정책 예시 관련 정보는 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023) 및 [버킷 정책 예시](https://intl.cloud.tencent.com/document/product/436/18031)를 참조하십시오. 다음은 버킷 정책 추가 방법에 대한 자세한 소개입니다.

>! 루트 계정당 버킷 ACL 규칙은 최대 1,000개까지 생성할 수 있습니다.

## 전제 조건

생성된 버킷에 대한 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309) 문서를 참조하십시오.

## 작업 순서


1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 메뉴에서 [버킷 리스트]를 클릭한 후, 버킷 정책 추가가 필요한 버킷을 선택해 버킷으로 이동합니다.
3. [권한 관리]를 클릭해 **Policy 권한 설정**을 찾습니다. COS는 버킷 정책 추가 방식으로 **그래픽 설정**과 **정책 구문**을 제공하며, 그중 하나의 방식을 선택해 버킷 정책을 추가할 수 있습니다. 설정 항목에 대한 설명은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참조하십시오.
   ![](https://main.qcloudimg.com/raw/3e3c1c923384785190720b8505e94025.png)
 - **그래픽 설정**
   설정 예시는 다음과 같습니다.
   ![](https://main.qcloudimg.com/raw/950c03ba2eb714c102b68b57d025792d.png)
 - **정책 구문**
   [편집]을 클릭해 정의한 정책 구문을 입력합니다. COS는 다양한 시나리오의 정책 구문을 제공합니다. 자세한 내용은 [버킷 정책 예시](https://intl.cloud.tencent.com/document/product/436/18031)를 참조하십시오.
     ![](https://main.qcloudimg.com/raw/b4e280ccbd67b081dcb59c4039f4d3b0.png)
4. 설정 정보에 오류가 없는지 확인한 후, [확인] 또는 [저장]을 클릭합니다. 이때 서브 계정을 사용해 COS 콘솔에 로그인하면 정책에 설정된 리소스 범위에 한해 액세스할 수 있습니다.
