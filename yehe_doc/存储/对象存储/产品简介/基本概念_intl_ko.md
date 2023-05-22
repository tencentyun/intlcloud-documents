
### 버킷(Bucket)

버킷은 객체 저장 수단으로 객체를 저장하는 ‘컨테이너’의 기능을 합니다. Tencent Cloud 콘솔, API, SDK 등 다양한 방식을 통해 버킷을 정적 웹 사이트 호스팅에 사용할지 설정하거나 액세스 권한 설정 등 버킷을 관리하고 속성을 설정할 수 있습니다.

관련 문서는 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312)를 참고하십시오.


### 객체(Object)

객체는 COS의 기본 단위로, 버킷(예: 사진 1장을 사진첩에 저장)에 저장됩니다. Tencent Cloud 콘솔, API, SDK 등 다양한 방식으로 객체를 관리할 수 있으며, API 및 SDK 사례에서 객체 이름 포맷은 &lt;ObjectKey>입니다.

관련 문서는 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.


### APPID

APPID는 Tencent Cloud 계정 신청 후 획득하게 되는 계정으로 시스템에서 자동으로 할당합니다. 변경 불가능한 고유 ID로, [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있습니다. Tencent Cloud 계정 APPID는 계정 ID와 유일하게 상응 관계를 갖는 애플리케이션 ID입니다.

APPID는 버킷 이름으로 자주 사용되며 전체 버킷 이름은 사용자 정의 문자열과 APPID로 구성되며 중간에 하이픈 ‘-’으로 연결됩니다. 예를 들어 `examplebucket-1250000000`의 1250000000이 APPID입니다.

### UID

이외에도 APPID는 임시 키를 생성하거나, 버킷 정책을 지정하거나, 액세스 관리 CAM에서 정책 설정 시 리소스 범위를 지정하는 데 사용되며, 이 때 APPID는 일반적으로 UID라 지칭하고 두 값은 동일합니다.

관련 문서는 [버킷 개요](https://intl.cloud.tencent.com/document/product/436/13312), [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023), [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606)를 참고하십시오.


### UIN

계정 ID를 말하며, APPID와 유일하게 상응 관계를 갖는 변경 불가능한 고유 ID입니다. [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있으며, COS 제품에 임시 키를 생성하거나, 버킷 정책을 지정하거나, 액세스 관리 CAM에서 정책 설정 시 리소스 범위를 지정하는 데 사용됩니다. 이 때 UID와 사용법이 유사하지만 접두사가 서로 다르므로 유의하십시오.

관련 문서는 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023), [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606)를 참고하십시오.

### ACL

액세스 제어 리스트(ACL)는 리소스를 기반으로 하는 액세스 관리 옵션 중 하나로, 액세스 권한 동작을 설명하는 데 사용됩니다.
COS에서 버킷 및 객체의 액세스를 관리하는 데 사용할 수 있습니다. ACL을 사용하여 다른 루트 계정 및 서브 계정, 사용자 그룹에 기본적인 읽기, 쓰기 권한을 부여할 수 있습니다.

관련 문서는 [액세스 제어 기본 개념](https://intl.cloud.tencent.com/document/product/436/30581), [ACL](https://intl.cloud.tencent.com/document/product/436/30583)을 참고하십시오.

### CORS

크로스 도메인 리소스 공유(Cross-Origin Resource Sharing, CORS)란 요청을 발송하는 리전과 해당 요청이 지정하는 리소스 소재 리전이 다른 HTTP 요청을 말합니다.


### SecretKey

SecretId와 SecretKey를 통칭하여 Cloud API 키라고 부르며, 사용자가 Tencent Cloud API에 액세스 시 인증할 때 사용하는 보안 자격 증명으로 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다. SecretKey는 서명 문자열 및 서버 인증 서명 문자열 키를 암호화하는 데 사용되며, APPID별로 여러 개의 Cloud API 키를 생성할 수 있습니다.


### SecretId

SecretId와 SecretKey를 통칭하여 Cloud API 키라고 부르며, 사용자가 Tencent Cloud API에 액세스 시 인증할 때 사용하는 보안 자격 증명으로 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다. SecretId는 API 호출자의 신분을 식별하는 데 사용되며, APPID별로 여러 개의 Cloud API 키를 생성할 수 있습니다.



### policy

정책(policy)은 몇 개의 요소로 구성되며, 권한의 구체적인 정보를 설명하는 데 사용합니다. 자세한 내용은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참고하십시오.


### 외부 네트워크 다운스트림 트래픽

데이터를 인터넷을 통해 COS에서 클라이언트로 전송할 때 발생하는 트래픽으로, 사용자가 직접 객체 링크를 통해 객체를 다운로드하거나 정적 웹 사이트 원본 서버를 통해 객체를 조회하는 데 발생하는 트래픽이 포함됩니다.

### CDN Origin-pull 트래픽
CDN(Content Delivery Network) origin-pull 트래픽은 COS에서 CDN 엣지 노드로의 데이터 전송에 의해 생성되는 트래픽입니다.


### 기본 도메인
COS 원본 서버 도메인으로, 버킷 생성 시 시스템에서 버킷 이름 및 리전에 따라 자동으로 생성하며 기본 가속 도메인 지역과 구분되어야 합니다. 자세한 내용은 [도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.


### 기본 CDN 가속 도메인

CDN 가속 노드를 경유하여 가속되는 도메인으로, 시스템이 기본으로 생성하며 사용자가 활성화 또는 비활성화를 선택할 수 있습니다. 자세한 내용은 [도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.


### 사용자 정의 CDN 가속 도메인
버킷에 ICP비안을 통과한 사용자 정의 도메인을 Tencent Cloud 중국 내 CDN 가속 플랫폼으로 바인딩할 수 있으며, 사용자 정의 도메인을 통해 버킷에 있는 객체에 액세스합니다. 자세한 내용은 [도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.


### 사용자 정의 원본 서버 도메인
ICP비안을 통과한 사용자 정의 도메인을 현재 버킷에 바인딩할 수 있으며, 사용자 정의 도메인을 통해 버킷에 있는 객체에 액세스합니다. 자세한 내용은 [도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.


### 데이터 검색
STANDARD IA 및 ARCHIVE 유형은 콜드 데이터 스토리지 유형입니다. STANDARD IA의 경우 해당 데이터 읽기 또는 다운로드 시 백그라운드에서 먼저 데이터를 검색한 후에 읽기 또는 다운로드할 수 있으며, ARCHIVE 데이터는 읽기 및 다운로드할 수 없고, 이 때의 데이터 검색을 데이터 동결 해제(즉, ARCHIVE 데이터를 STANDARD 데이터로 복구하는 과정)라고 합니다.


### 다중 AZ

다중 AZ(Multiple Availability Zones)은 Tencent Cloud COS에서 출시한 다중 AZ 스토리지 구성입니다. 사용자 데이터가 도시의 여러 데이터센터에 분산 저장되어 데이터센터 한 곳에 자연재해 및 정전 등 극단적인 상황이 발생하여 전체 장애가 발생하는 경우에도 사용자에게 안정적이고 신뢰도 높은 저장 서비스를 제공합니다.

관련 문서는 [Overview of Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208)를 참고하십시오.


### Region


Tencent Cloud 호스팅 데이터센터의 분포 지역으로, 리전이라고 하며 COS의 데이터가 해당 리전의 버킷에 저장됩니다.

관련 문서는 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.



