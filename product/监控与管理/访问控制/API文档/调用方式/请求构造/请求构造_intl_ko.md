Tencent Cloud에 대한 API 호출은 Tencent Cloud API의 서버 주소로 요청을 보내고 API 설명에 따라 요청에 해당 요청 매개변수를 추가하여 완료되는 것입니다. Tencent Cloud API의 요청 구조는 다음과 같은 부분으로 구성됩니다.

### 서비스 주소

Tencent Cloud API의 서비스 액세스 주소는 구체적인 모듈과 관련이 있습니다. 자세한 내용은 각 API에 대한 설명을 참조하십시오.

### 통신 프로토콜

Tencent Cloud API의 대부분 API는 HTTPS를 통해 통신하므로 매우 안전한 통신 연결을 제공합니다.

### 요청 방법

Tencent Cloud API는 POST 및 GET 요청을 모두 지원합니다.

> **주의: **1. 두 가지 요청 방법을 혼합할 수 없습니다. 즉, GET 방식을 사용하는 경우 매개변수는 Querystring에서 획득하고 POST 방식을 사용하면 매개변수는 Request Body에서 획득해야 합니다.
> Querystring의 매개변수는 무시됩니다. 두 가지 방식은 매개변수 포맷 규칙이 동일하지만 일반적으로 GET가 사용되며 매개변수 문자열이 너무 길면 POST가 권장됩니다. 2. 사용자의 요청 방법이 GET인 경우 모든 요청 매개변수 값을 URL 인코딩해야 하며 POST인 경우 매개변수를 인코딩할 필요가 없습니다.

### 요청 매개변수

Tencent Cloud API의 각 요청은 공통 요청 매개변수와 API 요청 매개변수를 지정해야 합니다. 그 중에 공통 요청 매개변수는 각 API에서 사용하는 요청 매개변수입니다. 자세한 내용은 [공통 요청 매개변수](https://cloud.tencent.com/document/api/213/11650) 섹션을 참조할 수 있습니다. API 요청 매개변수는 각 API에 고유한 것이며 자세한 내용은 각 API의 "요청 매개변수" 설명을 참조하십시오.

### 문자 인코딩

Tencent Cloud API 의 요청 및 리턴 결과는 UTF-8 문자 집합을 사용하여 인코딩됩니다.
