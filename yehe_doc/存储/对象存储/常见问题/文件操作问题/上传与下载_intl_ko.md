### COS에 업로드 및 다운로드 대역폭 제한이 있습니까?

중국대륙 공유 클라우드의 단일 버킷 리전 기본 대역폭은 15Gbit/s이며, 기타 리전은 10Gbit/s입니다. 대역폭이 임계값에 도달하면 요청을 통해 트래픽 제어가 트리거 됩니다. 더 큰 대역폭을 원하시면 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오. 

### 파일을 다운로드하지 않고 브라우저에서 미리보기하는 방법은 무엇입니까?

버킷 도메인 형식 ‘<BucketName-APPID>.cos.<Region>.myqcloud.com’은 XML 버전 도메인입니다. 브라우저에서 미리보기를 지원하는 유형의 파일이라면, 해당 형식의 도메인 객체 링크 액세스를 통해 브라우저에서 파일 미리보기가 가능합니다.

버킷 도메인 형식 `<BucketName-APPID>.<region>.myqcloud.com`은 JSON 버전 도메인입니다. JSON 버전 도메인에 상응하는 객체 링크 도메인은 브라우저에서 액세스할 때 다운로드 창이 팝업됩니다. 브라우저에서의 파일 미리보기는 다음 두 가지 방법이 있습니다. 

1. COS 콘솔 버전을 [신규 버전 콘솔](https://console.cloud.tencent.com/cos5)로 업그레이드하고, XML 버전 도메인에 상응하는 객체 링크를 통해 액세스합니다 (강력 권장).
2. 사용자 정의 도메인을 바인딩하고 정적 웹 사이트를 활성화하여 사용자 정의 도메인을 통해 액세스합니다. 관련 문서는 [JSON 버전 도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424)와 [JSON 버전 정적 웹 사이트 설정](https://intl.cloud.tencent.com/document/product/436/14984)을 참고하십시오.

#### 예시:

베이징 리전 도메인의 examplebucket-1250000000 버킷 루트 디렉터리의 picture.jpg 파일을 예로 들어 설명하겠습니다. 

- 객체 주소가 `https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg`형식인 경우, 해당 주소를 사용하여 브라우저에서 picture.jpg 파일을 미리보기할 수 있습니다.
- 객체 주소가 `https://examplebucket-1250000000.cosbj.myqcloud.com/picture.jpg`형식인 경우, 브라우저에서 미리보기는 다음 두 가지 방법이 있습니다. 
  1. COS 콘솔 버전을 [신규 버전 콘솔](https://console.cloud.tencent.com/cos5)로 업그레이드하고, XML 버전 도메인에 상응하는 객체 링크를 통해 액세스합니다 (강력 권장).
  2. 사용자 정의 도메인을 바인딩하고 정적 웹 사이트를 활성화하여 사용자 정의 도메인을 통해 액세스합니다. 관련 문서는 [JSON 버전 도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424)와 [JSON 버전 정적 웹 사이트 설정](https://intl.cloud.tencent.com/document/product/436/14984)을 참고하십시오.

### 파일을 미리보기 하지 않고 브라우저에서 다운로드하는 방법은 무엇입니까?

[COS 콘솔](https://console.cloud.tencent.com/cos5)을 통해 객체 사용자 정의 Headers의 Content-Disposition 매개변수 값을 attachment로 설정합니다. 콘솔 운영 가이드는 [사용자 정의 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참고하십시오.

GET Object 인터페이스에 요청 매개변수 response-content-disposition 값을 attachment로 설정하여 브라우저에서 파일 다운로드 창을 띄울 수도 있습니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 참고하십시오.

>! 요청에 response-* 매개변수를 사용하려면, 요청에 반드시 서명이 있어야 합니다. 

### 내부 네트워크를 통해 COS에 액세스 했는지 판단하는 방법은 무엇입니까?

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 리졸브를 사용하여 인터넷을 통해 다양한 통신사 환경에서 COS 액세스에 대한 최적의 링크를 점검 및 지정합니다. Tencent Cloud 내에 COS 액세스를 위한 서비스를 배포한 경우, 동일 리전 내 액세스는 자동으로 내부 네트워크 주소로 지정됩니다. 현재 리전 간 내부 네트워크 액세스는 지원하지 않으며, 기본적으로 외부 네트워크 주소로 리졸브 됩니다.

>! 공유 클라우드 리전과 금융 클라우드 리전 내부 네트워크는 서로 통신되지 않습니다.

#### 내부 네트워크 액세스 판단 방법

리전 내 Tencent Cloud 제품의 액세스는 자동으로 내부 네트워크를 사용하여 연결되며, 발생된 내부 네트워크 트래픽은 과금되지 않습니다. 그러므로 Tencent Cloud의 여러 제품을 구매할 경우, 비용 절감을 위해 최대한 같은 리전을 선택하실 것을 권장합니다.

내부 네트워크의 액세스 여부 확인은 다음 방법을 참고하십시오.

Tencent CVM을 통한 COS 액세스의 경우, 내부 인터넷을 이용하여 COS에 액세스했는지 판단하려면, CVM에서 `nslookup` 명령어를 사용하여 COS 도메인을 리졸브할 수 있습니다. 내부 IP를 반환한다면 CVM과 COS 간 내부 네트워크로 액세스한 것이고, 아니라면 외부 네트워크로 액세스한 것입니다.

>?내부 IP 주소는 일반적으로 `10.*.*.*`, `100.*.*.*` 형식이며, VPC 네트워크는 일반적으로 `169.254.*.*` 등입니다.

`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`이 타깃 버킷 주소라고 가정할 경우, 그 아래 `Address: 10.148.214.13`은 내부 네트워크에서 액세스했음을 의미합니다.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

내부 네트워크와 외부 네트워크 액세스 및 연결성 테스트에 관한 자세한 정보는[내부 네트워크와 외부 네트워크 액세스](https://intl.cloud.tencent.com/document/product/436/30613)를 참고하십시오. 

Tencent Cloud CVM 내부 네트워크 DNS 서버 주소는 [CVM 내부 네트워크 서비스](https://intl.cloud.tencent.com/document/product/213/5225)를 참고하십시오. 

>!Tencent Cloud BM 내부 IP 주소와 CVM IP 주소는 다르며, 일반적으로 `9.*.*.*`또는`10.*.*.*`형식입니다. 더 궁금하신 사항은 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.

### 폴더를 다운로드 하는 방법은 무엇입니까?

[COSBrowser 툴](https://intl.cloud.tencent.com/document/product/436/11366)에 로그인하여，다운로드할 폴더를 선택하고, [다운로드]를 클릭하면 폴더 다운로드 또는 파일 일괄 다운로드를 할 수 있습니다. 또는 COSCMD 툴을 통해서도 폴더를 다운로드 할 수 있습니다. 자세한 내용은 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 참고하십시오.

### 업로드 및 다운로드 시 '403 Forbidden', '권한 거부' 등 에러 메세지가 발생합니다. 어떻게 처리해야 합니까?

[COS 액세스 시 403 에러 코드 반환](https://intl.cloud.tencent.com/document/product/436/40105)문서를 참고하여 문제를 해결하십시오. 


### COS에서 파일 일괄 업로드 및 다운로드는 어떻게 합니까?

COS는 콘솔, API/SDK, 툴 등 다양한 방식을 통해 파일 일괄 업로드 또는 다운로드를 지원합니다.

- 콘솔 방식: 작업 순서는 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)를 참고하십시오.
- API/SDK 방식: COS는 프로그래밍을 통해 API 또는 SDK 인터페이스를 여러 번 호출하는 방식으로 배치 작업을 지원합니다. 자세한 내용은 [객체 업로드 API 인터페이스](https://intl.cloud.tencent.com/document/product/436/10111) 와 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참고하십시오.
- 툴 방식: [COSCMD 명령 라인 툴](https://intl.cloud.tencent.com/document/product/436/10976)과 [COSBrowser 툴](https://intl.cloud.tencent.com/document/product/436/11366)을 사용하여 배치 작업을 할 수 있습니다. 


### 파일을 버킷에 업로드할 때 동일한 이름의 파일이 존재하는 경우 덮어쓰기됩니까? 아니면 다른 버전의 파일이 새로 추가됩니까?

COS는 현재 버전 제어 기능을 지원합니다. 버킷에 버전 제어 기능이 활성화되어 있지 않은 경우 버킷에 동일한 이름의 파일을 업로드하면 이미 존재하는 동일한 이름의 파일을 덮어쓰기 하며, 버전 제어 기능을 활성화한 경우에는 해당 객체의 여러 버전이 동시에 존재할 수 있습니다.

### COS 멀티파트 업로드 방식의 최소 파트 크기는 어떻게 됩니까?

최소 파트 크기는 1MB입니다. 규격과 제한에 대한 자세한 사항은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 문서를 참고하십시오.

### 대용량 파일의 멀티파트 업로드 과정 중, 서명 효력 상실 후 서명을 바꿔서 계속 업로드할 수 있습니까?

가능합니다. 

### COS에 저장되어 있는 파일에 임시 URL을 생성하는 방법은 무엇입니까?

자세한 작업 방법은 [사전 서명 라이선스 다운로드](https://intl.cloud.tencent.com/document/product/436/14116)를 참고하십시오.


### 서명 유효 기간을 설정했는데 기간 만료 후에도 파일을 다운로드할 수 있는 이유는 무엇입니까?

기본적으로 브라우저는 로딩이 완료된 파일을 캐싱하기 때문에 같은 URL을 사용할 경우, 다시 서버에 요청을 하는 것이 아니라 캐시 결과를 반환합니다. 파일을 업로드할 때 Cache-Control: no-cache 헤더를 지정하여 브라우저 캐시를 차단할 것을 권장합니다. 자세한 내용은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 또는 [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746)문서를 참고하십시오. 또한 파일을 다운로드할 때 response-cache-control=no-cache 요청 매개 변수를 지정하여 브라우저 캐시를 차단할 수도 있습니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)문서를 참고하십시오.


### 콘솔에서 파일을 업로드할 때 ‘네트워크 문제로 인한 업로드 실패’ 메세지가 뜨면 어떻게 합니까?
해당 오류는 로컬 네트워크가 불안정하기 때문에 발생합니다. 네트워크를 변경해서 다시 업로드해 보시기 바랍니다.


### 다른 사람의 COS 파일 다운로드를 어떻게 차단합니까? 

버킷을 개인 읽기/쓰기로 설정할 수 있습니다. 자세한 내용은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)문서를 참고하십시오. 링크 도용 방지 화이트리스트 제한을 설정하여 리스트에 없는 도메인이 버킷의 기본 액세스 주소 액세스를 차단할 수도 있습니다. 자세한 내용은 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319)문서를 참고하십시오.

### 파일의 다운로드 URL에 영문 대소문자를 구별하지 않음을 설정할 수 있습니까? 

COS는 해당 기능을 지원하지 않습니다. COS 파일명은 영문 대소문자를 구별하며 URL을 통한 파일 액세스 역시 영문 대소문자를 구별합니다. 버킷에 CDN 가속 가능을 활성화 했다면 CDN 콘솔로 대소문자 무시 캐시 설정을 활성화하여 히트율을 높일 수 있습니다. 자세한 내용은 [대소문자 무시 캐시 설정](https://intl.cloud.tencent.com/document/product/228/35316)을 참고하십시오. 


### 파일 업로드 또는 버킷 생성 등 작업 진행 시, ‘your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)’ 에러 메세지가 뜨면 어떻게 처리합니까?

COS 루트 계정당 버킷 ACL 규칙 수는 최대 1000개입니다. 설정한 버킷 ACL 수가 1000개를 초과하는 경우 해당 오류가 발생하므로 사용하지 않는 ACL 규칙을 삭제하시기 바랍니다.
>?객체 레벨의 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우, ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하십시오.
