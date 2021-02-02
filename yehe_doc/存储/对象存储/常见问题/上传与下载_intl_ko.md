### COS에 업로드 및 다운로드 대역폭 제한이 있습니까?

중국대륙 공유 클라우드 리전의 기본 대역폭은 15Gbit/s이며, 기타 리전은 10Gbit/s입니다. 대역폭이 임계값에 이른 경우, 요청에 대해 트래픽 제어가 트리거됩니다. 더 넓은 대역폭이 필요한 경우 [Tecent Cloud A/S 엔지니어](https://console.cloud.tencent.com/workorder/category)에게 문의하십시오.

### 파일을 다운로드하지 않고 브라우저에서 직접 미리 볼 수 있습니까?

버킷 도메인 포맷 `<BucketName-APPID>.cos.<Region>.myqcloud.com`은 XML 버전 도메인입니다. 브라우저에서 직접 미리보기를 지원하는 파일 유형이라면 해당 포맷의 도메인에 상응하는 객체 링크에 액세스할 수 있으므로 브라우저에서 파일을 미리 볼 수 있습니다.


#### 예시:

베이징 리전의 examplebucket-1250000000 버킷의 루트 디렉터리에 있는 picture.jpg 파일을 예를 들면 다음과 같습니다.

객체 주소가 `https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg` 형식인 경우 직접 해당 주소를 사용하여 직접 브라우저에서 picture.jpg 파일을 미리 볼 수 있습니다.

### 파일을 미리 보지 않고 브라우저에서 직접 다운로드할 수 있습니까?

[COS 콘솔](https://console.cloud.tencent.com/cos5)을 통해 객체 사용자 정의 Headers의 Content-Disposition 매개변수 값을 attachment로 설정합니다. 콘솔 작업 가이드는 [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참조하십시오.

GET Object 인터페이스를 통해서도 설정할 수 있으며, 요청 매개변수 response-content-disposition 값을 attachment로 설정하면 파일 다운로드 창이 팝업됩니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 참조하십시오.

>! 요청 중 response-* 매개변수를 사용하려면 요청에 반드시 서명이 있어야 합니다.

### 내부 네트워크에서 COS에 액세스하는 것을 어떻게 판단합니까?

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 리졸브를 사용하여 인터넷을 통해 각각의 통신사 환경에서의 COS 액세스를 점검하고 최적의 링크를 제공합니다. Tencent Cloud 내부에 서비스를 배포하여 COS 액세스에 사용하는 경우 리전 내 액세스가 자동으로 내부 네트워크 주소로 바인딩됩니다. 현재 리전 간에는 내부 네트워크 액세스를 지원하지 않으며, 기본적으로 외부 네트워크 주소로 리졸브됩니다.

#### 내부 네트워크 액세스 판단 방법

리전 내 Tencent Cloud 제품 액세스는 자동으로 내부 네트워크를 사용하여 연결되며, 이 때 발생하는 내부 네트워크 트래픽은 과금되지 않습니다. 따라서 Tencent Cloud의 다른 제품을 선택하는 경우 최대한 동일한 리전을 선택하여 비용을 절감하시기 바랍니다.

내부 네트워크 액세스 여부 확인 방법은 다음을 참조하십시오.

Tencent CVM으로 COS에 액세스한다고 가정할 경우, 내부 네트워크를 사용하여 COS에 액세스하는지 여부 판단은 CVM 상에서 `nslookup` 명령어를 사용해 COS 도메인에 리졸브하여 내부 네트워크 IP가 리턴되면 CVM과 COS 사이에 내부 네트워크를 사용하여 액세스한 것이며, 내부 네트워크 IP가 아닌 경우 외부 네트워크를 사용하여 액세스한 것입니다.

>?내부 네트워크 IP 주소는 일반적으로 `10.*.*.*`, `100.*.*.*` 이며, VPC 네트워크는 일반적으로 `169.254.*.*` 등입니다.

예를 들어 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`이 타깃 버킷 주소인 경우, 다음 `Address: 10.148.214.13`은 내부 네트워크 액세스입니다.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

내부 네트워크 및 외부 네트워크, 연결성 테스트 등에 대한 자세한 정보는 [내부 네트워크 및 외부 네트워크 액세스](https://intl.cloud.tencent.com/document/product/436/30613)를 참조하십시오.

Tencent Cloud CVM 내부 네트워크 DNS 서버 주소는 [CVM 내부 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5225)를 참조하십시오.

>!Tencent Cloud CPM(Cloud Physical Machine) 내부 네트워크 IP 주소는 CVM IP 주소와 서로 상이하며, 일반적으로 `9.*.*.*` 또는 `10.*.*.*` 형식입니다. 문의사항은 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 확인하십시오.

### 폴더는 어떻게 다운로드합니까?

[COSBrowser 툴](https://intl.cloud.tencent.com/document/product/436/11366)에 로그인하여 다운로드할 폴더를 선택하고 [다운로드]를 클릭하면 폴더가 다운로드되거나 파일이 일괄 다운로드됩니다. 또는 COSCMD 툴을 통해서도 폴더를 다운로드할 수 있으며, 자세한 내용은 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 참조하십시오.

### 업로드 및 다운로드 시 “403 Forbidden” 및 권한 거절 등 오류가 발생합니다. 어떻게 처리해야 합니까?

다음 순서에 따라 문제를 진단하십시오.

1. 다음 정보가 정확하게 설정되어 있는지 확인합니다.
   BucketName, APPID, Region, SecretId, SecretKey 등
2. 상기 정보가 정확히 설정되어 있다는 전제 하에 서브 계정을 사용하여 작업했는지 확인하고, 서브 계정을 사용한 경우 루트 계정에서 서브 계정에 권한을 부여했는지 확인합니다. 권한을 부여하지 않은 경우 먼저 루트 계정으로 로그인하여 서브 계정에 권한을 부여합니다. 권한 부여 방법은 [액세스 권한 관리 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참조하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않으면 관련 Policy 설정을 수정합니다. 자세한 방법은 [임시 키 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.
4. 상기 순서에 따라 진행해도 문제를 해결할 수 없는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1)을 통해 문의하십시오.


### COS에서 파일 일괄 업로드 및 다운로드는 어떻게 합니까?

COS는 콘솔, API/SDK, 툴 등 다양한 방식을 통해 파일 일괄 업로드 또는 다운로드를 지원합니다.

- 콘솔 방식: 작업 순서는 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)를 참조하십시오.
- API/SDK 방식: COS는 프로그래밍을 통해 API 또는 SDK 인터페이스를 여러 번 호출하는 방식으로 배치 작업을 지원합니다. 자세한 내용은 [객체 업로드 API 인터페이스](https://intl.cloud.tencent.com/document/product/436/10111) 및 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참조하십시오.
- 툴 방식: [COSCMD TCCLI](https://intl.cloud.tencent.com/document/product/436/10976) 및 [COSBrowser 툴](https://intl.cloud.tencent.com/document/product/436/11366)을 사용하여 배치 작업을 실행할 수 있습니다.


### 파일을 버킷에 업로드할 때 이미 동일한 이름의 파일이 존재하는 경우 직접 덮어씁니까, 아니면 다른 버전의 파일을 새로 추가합니까?

COS는 현재 버전 제어 기능을 지원합니다. 버킷에 버전 제어 기능이 활성화되어 있지 않은 경우 버킷에 동일한 이름의 파일을 업로드하면 이미 존재하는 동일한 이름의 파일을 덮어쓰며, 버전 제어 기능을 활성화한 경우에는 해당 객체의 여러 버전이 동시에 존재할 수 있습니다.

### COS 멀티파트 업로드 방식의 최소 블록 크기는 어떻게 됩니까?

블록당 최소 크기는 1MB입니다. 자세한 내용은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 문서를 참조하십시오.

### 큰 파일을 멀티파트 업로드하는 과정에서 서명에 실패한 후 다시 서명을 변경하여 계속해서 멀티파트 업로드를 할 수 있습니까?

가능합니다.


### 콘솔에서 파일 업로드 시 "업로드 실패, 네트워크에 오류가 발생했습니다." 오류가 표시됩니다. 어떻게 해야 합니까?
해당 오류는 로컬 네트워크 환경이 불안정한 경우 표시됩니다. 네트워크 환경을 변경한 후 다시 업로드하시기 바랍니다.


### 다른 사람이 COS 파일을 다운로드하는 것을 방지하려면 어떻게 해야 합니까?

버킷을 개인 읽기/쓰기로 설정합니다. 자세한 방법은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315) 문서를 참조하십시오. 또는 링크 도용 방지를 통해서도 화이트리스트를 설정하여 리스트 이외의 도메인에서 버킷의 기본 액세스 주소에 액세스하는 것을 제한할 수 있으며, 자세한 방법은 [링크 도용 방지](https://intl.cloud.tencent.com/document/product/436/13319) 문서를 참조하십시오.


### 파일을 업로드하거나 버킷 생성 시 “your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)” 오류가 발생합니다. 어떻게 해야 합니까?

루트 계정당 COS 버킷 ACL 규칙 수는 최대 1000개입니다. 설정한 버킷 ACL 수가 1000개를 초과하는 경우 해당 오류가 발생하므로 사용하지 않는 버킷 ACL 규칙을 삭제하시기 바랍니다.

>?객체 등급별 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우 ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하는 것을 권장합니다.