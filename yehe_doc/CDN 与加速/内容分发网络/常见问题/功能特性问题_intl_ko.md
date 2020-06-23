### Tencent Cloud CDN은 중국 외 가속 기능이 있나요?
Tencent Cloud CDN은 중국 외 가속 기능을 지원합니다. Tencent Cloud CDN은 10년 이상 누적된 Tencent의 노드를 개방하여 1000개 이상의 중국 외 노드를 제공합니다. 전 세계 50개 이상의 국가 및 리전을 커버하여 귀하의 서비스가 해외에서도 원활하도록 지원합니다.

### CDN에 액세스한 후 원본 서버를 튜닝해야만 가속 서비스를 사용할 수 있나요?
일반적으로는 필요하지 않습니다. 그러나 더 나은 가속 효과를 위해서는 먼저 동적/정적 분리를 실행하는 것이 좋습니다. 동적 파일과 정적 파일에 다른 도메인을 할당하여 정적 리소스만 가속하면 됩니다.

### Tencent CDN은 크로스 도메인 액세스를 지원하나요?
Tencent Cloud CDN은 크로스 도메인을 제한 없이 액세스할 수 있습니다. 사용자의 웹 사이트에 크로스 도메인 액세스가 필요할 경우, 웹 사이트에서 Access-Control-Allow-Origin 필드를 설정하거나, CDN의 도메인을 크로스 도메인 헤더로 설정하여 액세스할 수 있습니다. 자세한 내용은 [HTTP Header 설정](https://intl.cloud.tencent.com/document/product/228/35320)을 참조 바랍니다.

### CDN 액세스 로그는 어디에서 다운로드할 수 있나요?
CDN 콘솔에서 CDN 액세스 로그를 다운로드할 수 있습니다. 자세한 작업 절차는 [로그 다운로드](https://intl.cloud.tencent.com/document/product/228/6316)를 참조 바랍니다.

### 장애 자가 진단 툴은 어떻게 사용하나요?
장애 자가 진단 툴은 액세스한 도메인의 DNS 리졸브, 링크 품질, 웹 사이트의 가용성, 데이터 일관성 등의 진단 항목을 점검하며, 자세한 작업 절차 [장애 자가 진단](https://intl.cloud.tencent.com/document/product/228/6304)을 참조 바랍니다. 진단 툴은 로컬 네트워크 환경 설정과 연관되어 있으므로 전체 네트워크의 진단 결과를 완벽히 나타내지는 않습니다.

### 로컬 액세스 진단과 사용자 액세스 진단의 차이점은 무엇인가요?
로컬 액세스 진단: 특정 리소스 액세스 중 오류가 발생할 경우, "로컬 액세스 진단"을 통해 점검을 시작할 수 있습니다.
사용자 액세스 진단: 사용자로부터 리소스 액세스의 오류 발생에 대한 문의를 받았을 경우, "사용자 액세스 진단"을 통해 문제를 찾은 뒤 Tencent Cloud가 제공하는 권장 작업에 따라 문제를 해결할 수 있습니다.

### CDN은 POST 요청을 지원하나요?
CDN은 POST 요청을 지원합니다.

### CDN은 원본 서버의 Cache-Control 설정을 지원하나요?
Tencent Cloud CDN은 원본 서버의 Cache-Control 설정을 기본적으로 지원합니다.

### CDN은 GZIP 압축을 지원하나요?
CDN에서는 트래픽을 절약하기 위해, 확장자가 .js;.html;.css;.xml;.json;.shtml;.htm;이고, 용량이 256Byte - 2048KB 사이인 파일에 대해 기본으로 Gzip 형식으로 압축합니다.

### CDN 가속은 80이 아닌 포트도 지원하나요?
현재 CDN 가속은 80, 443, 8080의 세 포트만 지원합니다.

### CDN 중간 서버란 무엇인가요?
CDN 중간 서버는 비즈니스 서버와 CDN 노드 사이에 위치하는 Origin-pull 중간 레이어 서버입니다. 중간 서버는 노드의 Origin-pull 요청을 수렴하여 원본 서버가 Origin-pull 시 받는 부하를 줄여줍니다.

### 클라이언트의 리얼 IP는 어떻게 수집하나요?
엣지 가속 노드를 통해 요청 시 클라이언트의 리얼 IP 정보가 있는 x-forward-for 헤더가 추가됩니다.

### CDN 서브 계정은 어떻게 설정하나요?
서브 계정 사용자가 Tencent Cloud에 가입하거나, CDN 서비스를 활성화할 필요 없이 CDN 생성자가 서브 계정 목록에 계정을 추가하면 됩니다. 서브 계정은 아래의 두 가지 유형으로 나눠집니다.
1. 정보 수신형.
2. 콘솔 사용형의 경우 다음의 링크를 통해 서브 계정 설정을 추가할 수 있습니다. [서브 계정 생성](https://intl.cloud.tencent.com/document/product/228/35229)

### CDN에서 IP 블랙리스트/화이트리스트 설정은 어떻게 하나요?
CDN이 IP 블랙리스트/화이트리스트 설정 기능을 제공합니다. 비즈니스에 맞게 사용자가 요청한 소스 IP의 필터 정책을 설정함으로써, 악성 IP의 도용 및 공격 등의 문제를 해결할 수 있습니다. 자세한 내용은 [IP 블랙리스트/화이트리스트 설정](https://intl.cloud.tencent.com/document/product/228/6298)을 참조 바랍니다.

구성 문제 더보기: [IP 액세스 빈도 제한 설정](https://intl.cloud.tencent.com/document/product/228/6420), [링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/228/6292)

### CDN에서 Range Origin-pull 설정은 어떻게 하나요?
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 왼쪽 메뉴바의 [Domain Management]를 선택한 뒤 편집할 도메인 오른쪽의 [Manage]를 클릭합니다. 자세한 내용은 [멀티 파트 원본 요청 설정](https://intl.cloud.tencent.com/document/product/228/7184)을 참조 바랍니다. 
![이미지 설명](https://main.qcloudimg.com/raw/d3e75f57d7731cedbbc55690fccf8e42.png)
[Origin Configuration]을 클릭하면 Range Origin-pull 설정 모듈을 볼 수 있습니다. ![이미지 설명](https://main.qcloudimg.com/raw/8a7e81c54c7cb0f950441759c0e62f48.png)

### CDN이 IP를 완벽히 숨길 수 없는 이유는 무엇인가요?
1. CDN 사용 전 IP가 이미 노출된 경우.
2. 기술적 수단으로 CDN을 사용할 경우 IP가 노출될 수 있습니다.
3. 서버상의 많은 웹 사이트 중 CDN을 사용하지 않는 도메인이 있을 때에도 노출될 수 있습니다.

### 핫 백업 원본 서버의 역할
메인 원본 서버가 외부 원본 서버인 경우 핫 백업 원본 서버를 추가할 수 있으며, 모든 원본 요청은 메인 원본 서버에 먼저 액세스합니다. 4XX, 5XX 에러 코드 출력, 링크 타임아웃, 프로토콜 비호환 등의 상황에서는 다시 핫 백업 원본 서버에 Origin-pull 하여 리소스를 가져옴으로써, 사용자가 Origin-pull을 효율적으로 사용할 수 있습니다.

### CDN은 top 도메인을 지원하지 않나요?
.pw 및 .top 도메인의 경우 CDN 액세스를 지원하지 않습니다.

### CDN에 파일을 업로드할 때 용량 제한이 있나요?
CDN 파일 업로드 시 파일 크기는 기본 32M 이내로 제한됩니다.

### Tencent Cloud CDN은 중국어 도메인을 지원하나요?
현재 Tencent Cloud CDN은 중국어 도메인을 지원하지 않습니다(트랜스 코딩도 지원 안 함).

### CDN Origin-pull이 내부 네트워크를 통과할 수 있나요?
현재 CDN Origin-pull은 공용 네트워크에서만 이동할 수 있습니다.
