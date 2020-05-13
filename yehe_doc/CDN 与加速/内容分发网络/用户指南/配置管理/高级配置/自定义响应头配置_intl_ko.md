## 설정 시나리오
사용자가 서비스 리소스를 요청할 때 리턴한 **응답 정보**에 사용자가 설정한 헤더를 추가하여 크로스 도메인 액세스 등을 구현할 수 있습니다.
HTTP Header 설정은 도메인을 위한 것이므로 설정이 적용되면 사용자는 해당 도메인 중 임의 리소스의 응답 정보에 설정 헤더를 추가할 수 있습니다. HTTP Header를 설정하면 클라이언트(예: 브라우저)의 응답 동작에만 영향을 미치며 CDN 노드의 캐싱 동작에는 영향을 미치지 않습니다.

## 설정 가이드
### 설정 조회
[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [Domain Management]를 선택하고 도메인 오른쪽의 [Manage]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. [Advanced Configuration]에서 HTTP Header 설정을 확인할 수 있으며 비활성화 상태로 기본 설정되어 있습니다.


### 설정 수정
#### 1. 설정 수정
on-off 스위치를 클릭하여 HTTP Header 설정을 추가하며 현재 아래와 같이 헤더 설정을 지정하거나 사용자 정의 헤더를 추가할 수 있습니다.
- Access-Control-Allow-Origin: 크로스 도메인 요청을 지정할 때 액세스 리소스의 요청 출처를 허용합니다.
- Access-Control-Allow-Methods: 크로스 도메인 요청을 지정할 때 허용된 크로스 도메인 요청 메서드입니다.
- Access-Control-Max-Age: 크로스 도메인 요청을 지정할 때, 특정 리소스에 대한 사전 요청 출력 결과의 캐시 시간입니다.
- Access-Control-Expose-Headers: 크로스 도메인 요청을 지정할 때 클라이언트가 확인할 수 있는 헤더 집합입니다.
- Content-Disposition: 클라이언트를 활성화하여 리소스를 다운로드하고 기본 파일명을 설정합니다.
- Content-Language: 페이지를 정의하는 데 사용되는 언어 코드입니다.
- 사용자 정의: 사용자 정의 헤더



**범용 설정: Content-Disposition**
Content-Disposition은 브라우저 다운로드를 활성화하고 기본 다운로드 파일명을 설정하는 데 사용됩니다. 서버가 클라이언트 브라우저에 파일을 발송할 때 TXT, JPG 등과 같이 브라우저에서 지원하는 파일 형식인 경우 기본적으로 브라우저에서 파일을 직접 열게 됩니다. 만약 사용자 저장이라는 알림 표시가 필요하면 Content-Disposition 필드 설정을 통해 브라우저 기본 동작을 덮어쓸 수 있습니다. 일반적인 설정은 다음과 같습니다.
`Content-Disposition：attachment;filename=FileName.txt`

**범용 설정: Content-Language**
Content-Language는 페이지를 정의하는 데 사용되는 언어 코드이며 일반적인 설정은 다음과 같습니다.
`Content-Language: zh-CN`
`Content-Language: en-US`

**크로스 도메인 설정: Access-Control-Allow-Origin**
크로스 도메인이란 어느 한 도메인을 가리킵니다. 예를 들어 `www.abc.com`의 어떤 리소스가 `www.def.com`이라는 도메인의 다른 리소스에 요청을 할 때, 리소스의 도메인 이름이 다르기 때문에, **크로스 도메인** 표시가 나타나게 됩니다. 프로토콜과 포트가 다르면 크로스 도메인 액세스 현상이 나타납니다. 이때 반드시 Response Header에서 크로스 도메인 관련 설정을 추가해야 데이터를 성공적으로 얻을 수 있습니다.
- 기능 소개:
Access-Control-Allow-Origin은 리소스의 크로스 도메인 권한 문제를 해결하는 데 사용됩니다. 도메인 값은 해당 리소스에 대한 액세스를 허용하는 도메인을 정의하며 최대 10개의 도메인 설정을 지원합니다. 출처가 도메인 이름 설정 목록 안에 호스트가 있기를 요청하면 해당 값을 리턴 헤더로 직접 입력합니다. 모든 도메인의 요청을 허용하도록 와일드카드 캐릭터 "*"를 설정할 수도 있습니다.
- 매칭 모드 소개

| **매칭 모드**   | **도메인 값**                                                     | **설명**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 풀 매칭         | *                                                            | * 로 설정될 때, 응답 시 헤더 추가: <br/>`Access-Control-Allow-Origin:*` |
| 고정 매칭       | `http://cloud.tencent.com`<br/> `https://cloud.tencent.com`<br/> `http://www.b.com` | 출처가 `https://cloud.tencent.com`이고 목록에 히트한 경우, 응답 시 헤더 추가: <br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>출처가 `https://www.qq.com`이고 목록에 히트하지 못한 경우, 응답에 변화가 없습니다. |
| 2급 와일드카드 서브도메인 매칭 | `http://*.tencent.com`                                       | 출처가 `https://cloud.tencent.com`이고 목록에 히트한 경우, 응답 시 헤더 추가: <br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>출처가 `https://cloud.qq.com`이고 목록에 히트하지 못한 경우, 응답에 변화가 없습니다. |
| 포트 매칭       |`https://cloud.tencent.com:8080`                             | 출처가 `https://cloud.tencent.com:8080`이고 목록에 히트한 경우, 응답 시 헤더 추가: <br/>`Access-Control-Allow-Origin:https://cloud.tencent.com:8080`<br/>출처가 `https://cloud.tencent.com`이고 목록에 히트하지 못한 경우, 응답에 변화가 없습니다. |

>특수 포트가 있는 경우 목록에서 관련 정보를 입력해야 하며 임의의 포트 매칭을 지원하지 않으므로 반드시 지정해야 합니다.

**크로스 도메인 설정: Access-Control-Allow-Methods**

Access-Control-Allow-Methods는 크로스 도메인에 적용되는 HTTP 요청 방법을 설정하는 데 사용되며 다음과 같이 여러 방법을 동시에 설정할 수 있습니다.
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

**크로스 도메인 설정: Access-Control-Max-Age**
Access-Control-Max-Age는 사전 요청의 유효 시간을 지정하는 데 사용됩니다.
비 단순 크로스 도메인 요청은 정식 통신 전에 크로스 도메인 요청이 안전하고 수용 가능한지 확인하기 위해 "사전 요청"이라는 HTTP 쿼리 요청을 추가해야 합니다. 다음의 요청은 비 단순 크로스 도메인 요청으로 간주됩니다.
- GET, HEAD 또는 POST 이외의 방식으로 시작하거나 POST를 사용하지만 요청 데이터 유형은 application / x-www-form-urlencoded, multipart / form-data, text / plain 이외의 데이터 유형, 예 application/xml 또는 text/xml인 경우.
- 사용자 정의 요청 헤더를 사용하는 경우.
Access-Control-Max-Age의 단위는 초입니다. 다음은 설정 예시입니다.
Access-Control-Max-Age:`1728000`

1728000초(20일) 내에 해당 리소스에 대한 크로스 도메인 액세스가 더는 다른 사전 요청을 보내지 않음을 나타냅니다.

**크로스 도메인 설정: Access-Control-Expose-Headers**
Access-Control-Expose-Headers는 응답의 일부로써 클라이언트에 노출될 수 있는 헤더를 지정하는 데 사용됩니다. 일반적으로 6종류의 헤더만 클라이언트에 노출될 수 있습니다.
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

클라이언트가 다른 헤더 정보에 액세스하도록 하려면 다음 설정을 통해 진행할 수 있습니다. 여러 헤더를 입력할 때는 ","로 구분해야 합니다.
`Access-Control-Expose-Headers: Content-Length,X-My-Header`
클라이언트가 Content-Length와 X-My-Header 두 헤더 정보에 액세스할 수 있음을 나타냅니다.

**사용자 정의 헤더**
사용자 정의 헤더 추가, 사용자 정의 key-value 설정을 지원합니다:

현재 다음의 Header 추가를 지원하지 않습니다.
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
여러 헤더가 중복으로 추가될 때 아래쪽의 우선 순위가 위쪽보다 높습니다. 따라서 가장 아래 부분의 설정이 바로 덮어쓰기 됩니다.

#### 2. 설정 비활성화
사용자는 HTTP Header 설정 on-off 스위치를 통해 원클릭으로 설정을 비활성화할 수 있으며 on-off 버튼이 비활성화 상태일 때 아래에 기존 설정이 존재하더라도 현재 네트워크에 적용되지 않습니다.


>가속 도메인 서비스 구역이 글로벌이면, 응답 헤더 설정이 글로벌 범위에 적용되며 중국 내, 중국 외를 다르게 설정할 수 없습니다.
