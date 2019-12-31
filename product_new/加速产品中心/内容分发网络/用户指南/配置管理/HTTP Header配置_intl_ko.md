Tencent Cloud에서 제공하는 HTTP header 구성 기능을 사용하십시오. 사용자가 비즈니스 리소스를 요청하면 반환된 **응답 메시지**에 구성된 헤더를 추가하여 크로스 도메인 방문 등 목적을 실현할 수 있습니다.
리소스가 노드에 도달되지 않으면 원본 가져오기가 진행됩니다. 이 때 원본 서버는 리턴된 헤더 정보는 사용자에게 함께 리턴합니다. 리소스가 노드에 캐시되면 정적 콘텐츠 가속, 가속 환경에서 CDN은 캐시된 원본 서버의 Access-Control-Allow-Origin, Timing-Allow-Origin, Content-Disposition, Accept-Ranges 헤더 정보를 사용자에게 리턴합니다.
HTTP header 구성은 도메인 이름을 위한 것이므로 구성이 적용되면 사용자는 구성된 헤더 도메인 이름 중 임의 자원의 리소스 정보에 구성 헤더를 추가할 수 있습니다. HTTP header를 구성하면 클라이언트(예: 브라우저)의 응답 동작에만 영향을 미치며 CDN 노드의 캐싱 동작에는 영향을 미치지 않습니다.

## 구성 안내
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 메뉴의 [도메인 관리]를 선택한 다음 편집할 도메인 이름의 오른쪽의 [관리]를 클릭하십시오.
2. [고급 구성]에서 [HTTP header 구성] 모듈을 찾으면 직접 헤더를 추가할 수 있습니다.
3. [HTTP header 추가]를 클릭하여 헤더를 추가하십시오.


CDN은 다음과 같은 일반적인 여섯 종류의 헤더 설정과 사용자 정의 헤더 설정을 제공합니다.
+ Content-Disposition: 클라이언트를 활성화하여 리소스를 다운로드하고 기본 파일명을 설정하십시오.
+ Content-Language: 페이지를 정의하는 데 사용되는 언어코드입니다.
+ Access-Control-Allow-Origin: 크로스 도메인 요청을 지정할 때 액세스 리소스의 요청 출처를 허용합니다.
+ Access-Control-Allow-Methods: 크로스 도메인 요청을 지정할 때 허용된 크로스 도메인 요청 방법입니다.
+ Access-Control-Max-Age: 크로스 도메인 요청을 지정할 때, 특정 리소스에 대한 사전 요청 반환 결과의 캐시 시간입니다.
+ Access-Control-Expose-Headers: 크로스 도메인 요청을 지정할 때 클라이언트가 확인할 수 있는 헤드 집합입니다.
+ 사용자 정의: 사용자 정의 헤더

### 범용 구성
#### Content-Disposition
Content-Disposition은 브라우저 다운로드를 활성화하고 기본 다운로드 파일명을 설정하는 데 사용됩니다. 서버가 클라이언트 브라우저에 파일을 발송할 때 TXT, JPG 등과 같이 브라우저에서 지원하는 파일 형식인 경우 기본적으로 브라우저에서 파일을 직접 열게 됩니다. 만약 사용자 저장이라는 메시지 표시가 필요하면 Content-Disposition 필드 구성을 통해 브라우저 기본 동작을 덮어쓸 수 있습니다. 일반적으로 구성은 다음과 같습니다:`Content-Disposition：attachment;filename=FileName.txt`

#### Content-Language
Content-Language는 페이지를 정의하는 데 사용되는 언어 코드이며 일반적인 구성은 다음과 같습니다.
`Content-Language: zh-CN`
`Content-Language: en-US`

### 크로스 도메인 구성
크로스 도메인이란 일정 도메인 이름을 가리킵니다. 예를 들어 ``` www.abc.com ``` 의 어떤 자원이 ```www.def.com ```이라는 도메인 이름의 다른 리소스에 요청을 할 때, 리소스의 도메인 이름이 다르기 때문에, **크로스 도메인** 표시가 나타나게 됩니다. 프로토콜과 포트가 다르면 크로스 도메인 액세스 현상이 나타납니다. 이 때 반드시 Response Header에서 크로스 도메인 관련 설정을 추가해야 데이터를 성공적으로 얻을 수 있습니다.

#### Access-Control-Allow-Origin
- 기능 소개
Access-Control-Allow-Origin은 리소스의 크로스 도메인 권한 문제를 해결하는 데 사용됩니다. 도메인 값은 해당 리소스에 대한 액세스를 허용하는 도메인을 정의하며 최대 10개의 도메인 구성을 지원합니다. 만약 출처 소스가 호스트가 도메인 이름 구성 목록 안에 있기를 요청하면 해당값을 반환 헤더로 직접 채웁니다. 모든 도메인의 요청을 허용하도록 와일드카드“*”를 설정할 수도 있습니다.
- 작업 절차
   1. CDN 콘솔에 로그인하고 [도메인 이름 관리] 페이지로 이동하여 설정하려는 도메인 이름을 선택한 다음 [관리]를 클릭하십시오.
   2. [고급 구성]에서 [HTTP header 구성] 모듈을 찾아 [HTTP header 추가]를 클릭하여 헤더를 추가하십시오.

> 최대 10개의 도메인 구성을 지원하고 1개에 1행, 엔터로 구분합니다.

- 매칭 모드 소개

| **매칭 모드**   | **도메인 값**   | **설명**    |
| -------------- | --------------------------- | ------------------------------------ |
| 전체 매칭         | *                                                            | * 설정 시,  response-header 에 헤더: Access-Control-Allow-Origins, 값은 ```*``` 추가하여 반환 |
| 고정 매칭       | ```http://www.test.com```<br/>```https://www.test.com```<br/>```http://www.b.com``` | <li> 출처소스가```https://www.test.com ```인 경우 목록에서 response-header 에 헤더 Access-Control-Allow-Origins, 값은:  ```https : // www.test.com``` 추가하여 반환</li><li> 출처 소스가 ```https://www.b.com ```인 경우 목록에 나오지 않으므로 response-header 에 헤더: Access-Control-Allow-Origins 추가할 필요 없이 반환</li>|
| 2레벨 광범위 도메인 이름 매칭 | ```http://*.test.com```                                      | <li> 소스가``http://www.test.com ''인 경우 매칭하고,  response-header 헤더에 Access-Control-Allow-Origins, 값은 ```http : // www.test.com```추가합니다.</li><li> 출처 소스가 ```https://www.test.com```인 경우 매칭이 되지 않으므로 response-header 헤더에 Access-Control-Allow-Origins 추가할 필요 없이 반환</li>|
| 포트 매칭 | ```https://www.test.com:8080```                               | <li> 출처 소스가``https://www.test.com:8080 ''인 경우 매칭하고, response-header에 헤더 Access-Control-Allow-Origins, 값: ```https : //www.test.com : 8080```추가하여 반환</li><li> 출처 소스가``https://www.test.com ```인 경우 매칭이 되지 않으므로 response-header에 헤더 Access-Control-Allow-Origins 추가할 필요 없이 반환</li>|

>! 특수 포트가 있는 경우 목록에서 관련 정보를 입력해야 하며 임의의 포트 매칭을 지원하지 않으므로 반드시 지정해야 합니다.

#### Access-Control-Allow-Methods 
Access-Control-Allow-Methods는 크로스 도메인에 적용되는 HTTP 요청 방법을 설정하는 데 사용되며 다음과 같이 여러 방법을 동시에 설정할 수 있습니다.
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

#### Access-Control-Max-Age
Access-Control-Max-Age는 사전 요청의 유효 시간을 지정하는 데 사용됩니다.
비정규 크로스 도메인 요청은 정식 통신 전에 교차 요청이 안전하고 수용 가능한지 확인하기 위해 "사전 요청"이라는 HTTP 쿼리 요청을 추가해야 합니다. 이하의 요청은 비정규의 크로스 도메인 요청으로 간주됩니다.
+ GET, HEAD 또는 POST 이외의 방식으로 시작하거나 POST를 사용하지만 요청 데이터 유형은 application/x-www-form-urlencoded, multipart/form-data, text/plain 이외의 데이터 유형, 예: application/xml 또는 text/xml.
+ 사용자 정의 요청 헤더를 사용하십시오.

Access-Control-Max-Age의 단위는 초입니다. 다음은 설정 예시입니다.
Access-Control-Max-Age:` 1728000`

1728000초(20일) 내에 해당 리소스에 대한 크로스 도메인 액세스가 더 이상 다른 사전 요청을 보내지 않음을 나타냅니다.

#### Access-Control-Expose-Headers
Access-Control-Expose-Headers는 응답의 일부로 클라이언트에 노출 될 수 있는 헤더를 지정하는 데 사용됩니다. 일반적으로 6종류의 헤더만 클라이언트에 노출 될 수 있습니다.
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

클라이언트가 다른 헤더 정보에 액세스하도록 하려면 다음 설정을 통해 진행할 수 있습니다. 여러 헤더를 입력할 때는 ","로 구분해야 합니다.
> Access-Control-Expose-Headers: Content-Length,X-My-Header

클라이언트가 Content-Length와 X-My-Header 두 헤더 정보에 액세스할 수 있음을 나타냅니다.

### 사용자 정의 헤드

사용자 정의 header 추가, 사용자 정의 key-value 설정 지원:

현재 다음의 header 추가를 지원하지 않습니다.

```
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```

여러 헤더가 중복으로 추가되면 하위 우선 순위가 위쪽 우선순위보다 높아집니다. 따라서 최하위 부분의 구성은 덮어쓰기 됩니다.

