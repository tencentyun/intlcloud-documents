## 소개
COS는 객체 차원에 따른 액세스 권한 설정을 제공하며 이 권한은 버킷 액세스 권한보다 우선순위가 높습니다.

>
>- 객체의 액세스 권한은 사용자가 기본 도메인을 통해 액세스할 시에만 유효합니다. CDN 가속 도메인과 사용자 정의 도메인을 통해 액세스할 시 버킷 액세스 권한을 기준으로 합니다.
>- 액세스 정책 규칙에는 수량 제한이 존재합니다. 자세한 내용은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518)을 참조하십시오.

## 작업 순서




1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 왼쪽 메뉴의 [버킷 리스트]를 클릭하여 버킷 리스트 항목으로 이동합니다.
2. 객체 액세스 권한이 필요한 버킷을 찾아 버킷 이름을 클릭하여 버킷에 있는 상세 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/156823c7ad23708feb85f5d682c61d50.png)
3. 버킷에 있는 상세 페이지의 [파일 리스트]에서 권한 설정이 필요한 객체를 찾고 오른쪽의 [자세히]를 클릭하여 파일 상세 페이지로 이동합니다. (폴더의 경우 오른쪽의 [권한 설정]을 클릭)
![](https://main.qcloudimg.com/raw/6065855393a30c809d60b4d0027628a6.png)
4. 상단의 [객체 권한]설정 항목을 클릭하고 실제 수요에 따라 액세스 권한을 설정합니다. 서브 계정에 객체 권한을 부여한 경우 서브 계정 ID는 [액세스 관리](https://console.cloud.tencent.com/cam) 콘솔에서 조회할 수 있습니다. COS는 객체 설정에서 권한 유형 2가지를 지원합니다.
 - **공용 권한**: 권한 상속, 개인 읽기, 공개 읽기 및 개인 쓰기를 포함합니다. 공용 권한에 대한 설명은 객체 개요에서 [권한 분류](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오.
 - **사용자 권한**: 루트 계정의 기본 값은 객체의 모든 권한 소유(전체 제어)로 설정되어 있습니다. 그 외에도 COS는 서브 계정을 추가하여 데이터 읽기/쓰기, 권한 읽기/쓰기, **전체 제어할** 수 있는 최고 권한까지 부여할 수 있습니다.
![](https://main.qcloudimg.com/raw/c9565ab1d2378ce672a301843bf3b072.png)
5. 마지막으로 [저장]을 클릭하면 객체의 액세스 권한이 설정됩니다.
6. 여러 개체의 일괄 설정이나 액세스 권한을 수정해야 할 경우 여러 객체를 선택한 후 [더 많은 조작]에서 [액세스 권한 수정]을 선택합니다.
![](https://main.qcloudimg.com/raw/a00d8522c2698c39aa4687463bcb05e4.png)

