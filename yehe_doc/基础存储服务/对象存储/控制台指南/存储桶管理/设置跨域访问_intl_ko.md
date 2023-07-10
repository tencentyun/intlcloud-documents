## 소개

Cloud Object Storage(COS) 콘솔에서 버킷의 객체에 대해 교차 출처 리소스 공유(Cross-Origin Resource Sharing, CORS)를 설정할 수 있습니다. COS는 OPTIONS 요청에 응답하기 위해 여러 규칙 구성을 지원합니다. CORS는 HTTP 요청을 통해 한 출처의 리소스를 다른 출처에서 요청할 수 있도록 하는 메커니즘입니다. 프로토콜, 도메인 이름 또는 포트가 다른 한 origin은 서로 다른 것으로 간주됩니다.

COS 서비스는 크로스 도메인 간 액세스를 위한 OPTIONS 요청 응답 기능을 지원하며, 개발자가 설정한 규칙에 따라 브라우저로 세부 설정 규칙을 반환합니다. 하지만 이후 실행되는 크로스 도메인 요청이 규칙에 부합하는지 여부는 서버에서 검사하지 않습니다. 자세한 내용은 [HTTP 액세스 제어에 관한 설명](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)과 [CORS 설정](https://intl.cloud.tencent.com/document/product/436/11488)의 모범 사례 문서를 참고하십시오.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭합니다.
3. CORS를 설정할 버킷의 이름을 클릭하여 버킷 상세 페이지로 이동합니다.
4. 왼쪽 사이드바에서 **보안 관리 > CORS**를 선택하고 **규칙 추가**를 클릭합니다.
![](https://main.qcloudimg.com/raw/1659089c942ec8fadd77c880f1d4f492.png)
5. 규칙 정보를 구성합니다(*로 표시된 필드는 필수). 구성 항목은 다음과 같습니다.
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
 - **Origin**: CORS 요청이 허용되는 소스입니다. 도메인 이름과 IP 주소를 추가할 수 있습니다.
    - 도메인 이름은 슬래시`/`로 끝날 필요가 없습니다.
    - 한 줄에 하나씩 여러 도메인 이름을 지정할 수 있습니다.
    - `*`가 지원되어 모든 도메인 이름과 IP 주소가 허용됨을 나타내므로 권장하지 않습니다.
    - `http://www.abc.com` 형식의 단일 특정 도메인 이름이 지원됩니다.
    - `http://*.abc.com` 형식의 두 번째 레벨 와일드카드 도메인 이름이 지원되지만 각 줄에는 `*`가 하나만 포함될 수 있습니다.
    - 프로토콜 이름 http 또는 https를 생략하지 않도록 주의하십시오. 포트가 기본 포트 80이 아닌 경우 포트도 포함해야 합니다. 예시 IP 주소는 `http://10.10.10.10`입니다.
 - **Allow-Methods**: GET, PUT, POST, DELETE 및 HEAD가 지원됩니다. 하나 이상의 허용된 CORS 요청 방법을 열거할 수 있습니다.
 - **Allow-Headers**: OPTIONS 요청을 통해 후속 요청에서 어떤 사용자 정의 HTTP 헤더(예시: x-cos-meta-md5)가 허용되는지 서버에 알립니다.
    - 한 줄에 하나씩만 여러 Headers를 지정할 수 있습니다. 예시: Content-Type.
    - Header는 생략되는 경향이 있으며 달리 필요하지 않은 경우 모든 헤더가 허용됨을 나타내는 `*`로 설정하는 것이 좋습니다.
    - 영어 대소문자 [a-z, A-Z]가 지원되지만, 언더바 `_`는 허용되지 않습니다.
    - Access-Control-Request-Headers에 지정된 각 Header는 Allowed-Header의 값과 일치해야 합니다.
 - **Expose-Headers**: Expose-Header는 COS의 상용 Header를 반환합니다. 자세한 내용은 [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728)를 참고하십시오. 실제 상황에 맞춰 세부 설정을 할 수 있으며, 기본값으로 Etag 입력을 권장합니다. 임의 문자 기호는 허용하지 않으며, 대소문자를 구분하지 않습니다. 다수 행을 생성할 수 있으나, 각 행에는 한 개만 입력할 수 있습니다.
 - **Max-Age**: OPTIONS 요청으로 얻은 결과의 유효 기간(초). 값은 600과 같은 양의 정수여야 합니다.
 - **Vary: Origin 반환**: Vary: Origin Header 반환 여부를 설정합니다. 브라우저에 CORS와 비 CORS 요청이 동시에 있는 경우 이 옵션을 활성화하십시오. 그렇지 않으면 도메인 간 문제가 발생할 수 있습니다.
 >!'Vary: Origin'을 선택하면 브라우저 액세스 또는 CDN Origin-pull이 증가할 수 있습니다.
6. 구성을 완료한 후 **저장**을 클릭하면 CORS 규칙이 추가된 것을 볼 수 있습니다. 수정하려면 **수정**을 클릭합니다.
![](https://main.qcloudimg.com/raw/c4399193611b4f81e57a549634ea865a.png)
