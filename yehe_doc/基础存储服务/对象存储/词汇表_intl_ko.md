COS를 효과적으로 이용하는 데 도움이 되는 기본 개념과 용어를 소개합니다.
### 버킷
버킷(Bucket)은 COS에서 객체 저장을 위해 사용됩니다. 버킷 하나에 다수의 객체를 저장할 수 있습니다. 버킷명은 사용자 정의한 문자열과 시스템에서 자동 생성된 숫자열을 하이픈으로 연결해 생성하고, 버킷명은 글로벌하게 고유해야 합니다. 자세한 내용은 [버킷 관리](/document/product/436/13312)를 참조하십시오.
### 객체
객체(Object)는 COS의 기본 저장 단위입니다. 자세한 내용은 [객체 관리](/document/product/436/13324)를 참조하십시오.
### 리전
리전(Region)은 COS의 데이터센터가 소재한 지역을 뜻합니다. 사용자는 요금과 요청 출처 등을 종합적으로 판단해 데이터 스토리지의 리전을 선택할 수 있습니다. 객체의 업로드 및 다운로드 속도 확보를 위해 본인의 업무 시나리오와 인접한 리전 스토리지를 선택하는 것을 권장합니다. 자세한 내용은 [리전 및 액세스 도메인](/document/product/436/6224)을 참조하십시오.
리전은 버킷을 생성할 때 지정하며, 지정한 뒤에는 변경할 수 없습니다. 버킷에 저장된 모든 객체는 버킷에 할당한 데이터센터에 저장됩니다. 현재 객체 레벨에 따른 리전 설정은 지원하지 않습니다.
### APPID
APPID는 Tencent Cloud 계정의 식별자로서 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정을 신청하면 사용자에게 APPID 1개가 자동 할당됩니다. APPID는 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/developer)의 [계정 정보]에서 조회할 수 있습니다.
### API 키
API 키는 사용자가 Tencent Cloud API에 액세스하여 본인 인증을 할 때 사용되는 보안 자격 증명이며, SecretId와 SecretKey로 구성됩니다. 사용자 계정 하나당 여러 개의 Tencent Cloud API 키를 생성할 수 있습니다. Tencent Cloud API 키가 없는 사용자는 [Tencent Cloud API 키 콘솔](https://console.cloud.tencent.com/capi)에서 생성할 수 있습니다. Tencent Cloud API 키가 없으면 Tencent Cloud API 인터페이스를 호출할 수 없습니다.
### SecretId 
SecretId는 Tencent Cloud API 키의 구성 요소로서 API 호출자의 신분을 식별합니다.
### SecretKey
SecretKey는 Tencent Cloud API 키의 구성 요소로서 서명 문자열 암호화 및 서버의 서명 문자열 인증에 사용됩니다.
### 기본 액세스 도메인
기본 액세스 도메인은 버킷명, COS 소재지 표시, 객체명으로 이루어져 있으며, 기본 액세스 도메인으로 COS의 유일한 대응 객체의 주소를 지정할 수 있습니다. Tencent Cloud는 사용자가 객체를 업로드하면 객체의 기본 액세스 도메인을 자동 생성합니다. 자세한 내용은 도메인 관리를 참조하십시오.
### CDN 가속 액세스 도메인
CDN 가속 액세스 도메인은 버킷명, CDN 가속 표시, 객체명으로 이루어져 있으며, 이 도메인으로 COS의 유일한 대응 객체의 주소를 지정할 수 있습니다. Tencent Cloud는 사용자가 객체를 업로드하고, CDN 가속을 실행하면 객체의 CDN 가속 액세스 도메인을 생성합니다. CDN 가속 액세스 도메인은 전국에 분포한 가속 노드를 통해 가속 액세스할 수 있으며, 자세한 내용은 [CDN 가속 설정](https://cloud.tencent.com/document/product/436/18424)을 참조하십시오.
