### COS에 업로드 및 다운로드 대역폭 제한이 있습니까?

중국 본토의 퍼블릭 클라우드 리전의 각 버킷 기본 대역폭: 업스트림 및 다운스트림 15Gbit/s 공유, 기타 리전: 10Gbit/s입니다. 이 임계값에 도달하면 트래픽 제한이 트리거됩니다. 자세한 내용은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518)을 참고하십시오.

### 파일을 다운로드하지 않고 브라우저에서 직접 미리 보려면 어떻게 해야 하나요?

이 파일에 대해 올바른 Content-Type 헤더를 지정해야 합니다. 또한 Content-Disposition 값은 attachment가 될 수 없습니다. 브라우저가 현재 파일 형식을 지원하는 경우 파일을 다운로드하는 대신 파일을 직접 엽니다. 자세한 지침은 [사용자 지정 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참고하십시오.

### 파일을 미리 보지 않고 브라우저에서 직접 다운로드하려면 어떻게 해야 하나요?

[COS 콘솔](https://console.cloud.tencent.com/cos5)로 이동하여 사용자 지정 객체 Headers의 Content-Disposition 매개변수 값을 attachment로 설정할 수 있습니다. 자세한 지침은 [사용자 지정 Headers](https://intl.cloud.tencent.com/document/product/436/13361)를 참고하십시오.

GET Object 인터페이스에 요청 매개변수 response-content-disposition 값을 attachment로 설정하여 브라우저에서 파일 다운로드 창을 띄울 수도 있습니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 참고하십시오.

>! 요청에 response-* 매개변수를 사용하려면, 요청에 반드시 서명이 있어야 합니다. 
>

### 사설망을 통해 COS에 액세스하고 있는지 어떻게 확인합니까?

Tencent Cloud COS의 액세스 도메인은 스마트 DNS 레졸루션을 사용하여 각 통신사 환경의 인터넷에서 COS 액세스를 검증하고 최적의 링크를 제공합니다.

Tencent Cloud에 배포한 CVM 서비스가 사설망에서 COS에 액세스하려면, 먼저 CVM과 COS 버킷이 동일한 리전에 속하는지 확인한 후 CVM에서 `nslookup` 명령을 사용하여 COS 도메인 이름을 해석해야 합니다. 내부 IP가 반환되면 CVM과 COS 간에 사설망 액세스를 나타내고, 그렇지 않으면 공중망 액세스를 나타냅니다.

Tencent Cloud에서 배포한 CVM 서비스의 리전이 COS 버킷이 속한 리전과 다르지만, COS 사용 가능 리전 범위 내에 있는 경우, COS 사설망 전역 가속 도메인 이름을 통해 파일에 액세스하여 CVM과 COS의 리전 간 액세스를 구현할 수 있습니다.

#### 사설망을 통한 액세스를 판단하는 방법

동일한 리전 내의 Tencent Cloud 제품은 사설망을 통해 서로 액세스할 수 있으므로 트래픽 비용이 발생하지 않습니다. 따라서 비용을 절약하기 위해 다른 Tencent Cloud 제품을 구매할 때 동일한 리전을 선택하는 것이 좋습니다.

>! 퍼블릭 클라우드 리전의 사설망은 금융 클라우드 리전의 사설망과 상호 연결되지 않습니다.
>

다음은 사설망을 통한 액세스를 확인하는 방법입니다.

예를 들어, CVM(Cloud Virtual Machine)이 COS(Cloud Object Storage)에 액세스할 때 사설망이 액세스에 사용되는지 확인하려면 CVM에서 `nslookup` 명령을 사용하여 COS 엔드포인트를 확인합니다. 사설망 IP가 반환되면 CVM과 COS 간의 액세스는 사설망을 통해 이루어집니다. 그렇지 않으면 공중망을 통해 이루어집니다.

>? 일반적으로 사설망 IP 주소는 `10.*.*.*` 또는 `100.*.*.*` 형식이며, VPC IP 주소는 `169.254.*.*` 형식입니다.
>

`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com`이 대상 버킷 주소라고 가정합니다. 아래의 `Address: 10.148.214.13`은 사설망에서 액세스했음을 의미합니다.

```shell
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com

Server:         10.138.224.65
Address:        10.138.224.65  #53

Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.13
Name:   examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Address: 10.148.214.14
```

사설망과 공중망 액세스 및 연결성 테스트에 관한 자세한 정보는[사설망과 공중망 액세스](https://intl.cloud.tencent.com/document/product/436/30613)를 참고하십시오. 

Tencent Cloud CVM 사설망 DNS 서버 주소는 [CVM 인트라넷 서비스](https://intl.cloud.tencent.com/document/product/213/5225)를 참고하십시오.

>! Tencent Cloud BM 사설망 IP 주소와 CVM IP 주소는 다르며, 일반적으로 `9.*.*.*` 또는 `10.*.*.*`형식입니다. 더 궁금하신 사항은 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
>

### 폴더를 다운로드 하는 방법은 무엇입니까?

[COSBrowser 툴](https://intl.cloud.tencent.com/document/product/436/11366)에 로그인하여，다운로드할 폴더를 선택하고, **다운로드**를 클릭하면 폴더 다운로드 또는 파일 일괄 다운로드를 할 수 있습니다. 또는 COSCMD 툴을 통해서도 폴더를 다운로드 할 수 있습니다. 자세한 내용은 [COSCMD 툴](https://intl.cloud.tencent.com/document/product/436/10976)을 참고하십시오.

### 업로드 및 다운로드 시 '403 Forbidden', '권한 거부' 등 에러 메세지가 발생합니다. 어떻게 처리해야 합니까?

[COS 액세스 시 403 에러 코드 반환](https://intl.cloud.tencent.com/document/product/436/40105) 문서를 참고하여 문제를 해결하십시오.


### COS에서 파일 일괄 업로드 및 다운로드는 어떻게 합니까?

COS는 콘솔, API/SDK, 툴 등 다양한 방식을 통해 파일 일괄 업로드 또는 다운로드를 지원합니다.

- 콘솔: 자세한 사용법은 [객체 업로드](https://intl.cloud.tencent.com/document/product/436/13321)와 [객체 다운로드](https://intl.cloud.tencent.com/document/product/436/13322)를 참고하십시오.
- API/SDK: COS를 사용하면 API 또는 SDK를 반복적으로 호출하여 여러 파일에서 작업할 수 있습니다. 자세한 내용은 [객체 업로드/다운로드](https://intl.cloud.tencent.com/document/product/436/10111) 와 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참고하십시오.
- 툴: [COSBrowser](https://intl.cloud.tencent.com/document/product/436/11366), [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976) 또는 [COSCLI](https://intl.cloud.tencent.com/document/product/436/43249)를 사용하여 일괄 작업을 구현할 수 있습니다.


### 파일을 버킷에 업로드할 때 동일한 이름의 파일이 존재하는 경우 덮어쓰기됩니까? 아니면 다른 버전의 파일이 새로 추가됩니까?

COS는 현재 버전 제어 기능을 지원합니다. 버킷에 버전 제어 기능이 활성화되어 있지 않은 경우 버킷에 동일한 이름의 파일을 업로드하면 이미 존재하는 동일한 이름의 파일을 덮어쓰기 하며, 버전 제어 기능을 활성화한 경우에는 해당 객체의 여러 버전이 동시에 존재할 수 있습니다.

### COS 멀티파트 업로드 방식의 최소 파트 크기는 어떻게 됩니까?

최소 파트 크기는 1MB입니다. 규격과 제한에 대한 자세한 사항은 [규격 및 제한](https://intl.cloud.tencent.com/document/product/436/14518) 문서를 참고하십시오.

### 대용량 파일의 멀티파트 업로드 과정 중, 서명 효력 상실 후 서명을 바꿔서 계속 업로드할 수 있습니까?

가능합니다. 

### COS에 저장되어 있는 파일에 임시 URL을 생성하는 방법은 무엇입니까?

자세한 작업 방법은 [사전 서명된 URL을 통해 다운로드](https://intl.cloud.tencent.com/document/product/436/14116)를 참고하십시오.


### 서명 유효 기간을 설정했는데 기간 만료 후에도 파일을 다운로드할 수 있는 이유는 무엇입니까?

기본적으로 브라우저는 로딩이 완료된 파일을 캐싱하기 때문에 같은 URL을 사용할 경우, 다시 서버에 요청을 하는 것이 아니라 캐시 결과를 반환합니다. 파일을 업로드할 때 Cache-Control: no-cache 헤더를 지정하여 브라우저 캐시를 차단할 것을 권장합니다. 자세한 내용은 [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) 또는 [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) 문서를 참고하십시오. 또한 파일을 다운로드할 때 response-cache-control=no-cache 요청 매개 변수를 지정하여 브라우저 캐시를 차단할 수도 있습니다. 자세한 내용은 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) 문서를 참고하십시오.


### 콘솔에서 파일을 업로드할 때 ‘네트워크 문제로 인한 업로드 실패’ 메세지가 뜨면 어떻게 합니까?
해당 오류는 로컬 네트워크가 불안정하기 때문에 발생합니다. 네트워크를 변경해서 다시 업로드해 보시기 바랍니다.


### 다른 사람의 COS 파일 다운로드를 어떻게 차단합니까? 

버킷을 개인 읽기/쓰기로 설정할 수 있습니다. 자세한 내용은 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315) 문서를 참고하십시오. 링크 도용 방지 얼로우리스트 제한을 설정하여 리스트에 없는 도메인이 버킷의 기본 액세스 주소 액세스를 차단할 수도 있습니다. 자세한 내용은 [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/436/13319) 문서를 참고하십시오.

### 파일의 다운로드 URL에 영문 대소문자를 구별하지 않음을 설정할 수 있습니까? 

COS는 해당 기능을 지원하지 않습니다. COS 파일명은 영문 대소문자를 구별하며 URL을 통한 파일 액세스 역시 영문 대소문자를 구별합니다. 버킷에 CDN 가속 가능을 활성화 했다면 CDN 콘솔로 대소문자 무시 캐시 설정을 활성화하여 히트율을 높일 수 있습니다. 자세한 내용은 [대소문자 무시 캐시 설정](https://intl.cloud.tencent.com/document/product/228/35316)을 참고하십시오.


### 파일 업로드 또는 버킷 생성 등 작업 진행 시, ‘your policy or acl has reached the limit (Status Code: 400; Error Code: PolicyFull)’ 에러 메세지가 뜨면 어떻게 처리합니까?

COS 루트 계정당 버킷 ACL 규칙 수는 최대 1000개입니다. 설정한 버킷 ACL 수가 1000개를 초과하는 경우 해당 오류가 발생하므로 사용하지 않는 ACL 규칙을 삭제하시기 바랍니다.
>? 객체 레벨의 ACL 또는 Policy 사용은 권장하지 않습니다. API 또는 SDK 호출 시 파일에 특별한 ACL 제어가 필요 없는 경우, ACL 관련 매개변수(예: x-cos-acl, ACL 등)는 비워 놓고 버킷 권한 상속을 유지하십시오.
>


