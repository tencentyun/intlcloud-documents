## 설정 시나리오

서비스 사용자가 서비스 리소스를 요청할 때 반환된 **응답 메시지**에 헤더를 설정하여 크로스 도메인 액세스 등을 구현할 수 있습니다.
응답 헤더는 도메인 차원에서 설정하므로 설정이 적용되면 도메인 하의 모든 리소스의 응답 메시지에 적용됩니다. 응답 헤더 설정은 클라이언트(예: 브라우저)의 응답 동작에만 영향을 미치며, CDN 노드의 캐싱 동작에는 영향을 미치지 않습니다.

## 설정 가이드

### 설정 조회

[CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하여 메뉴바에서 [도메인 관리]를 선택하고 도메인 오른쪽의 [관리]를 클릭하면 도메인 설정 페이지로 이동할 수 있습니다. [고급 설정]에서는 응답 헤더 설정을 확인할 수 있습니다. 기본적으로 비활성화 상태로 설정되며, [규칙 추가]를 클릭하면 HTTP 응답 헤더 규칙을 설정할 수 있습니다.
![](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### 작업 유형

| 작업 유형 | 설명                                                         |
| :------- | :----------------------------------------------------------- |
| 설정     | 지정된 응답 헤더 매개변수의 값을 설정 완료 후의 값으로 변경합니다. <br/>설정된 헤더가 존재하지 않을 경우, 해당 헤더를 추가합니다. <br>중복된 헤더 매개변수가 다수 존재할 경우, 모두 하나의 헤더로 통합됩니다. 즉, 설정 규칙이 [x-cdn: value1 설정]인 경우, 요청에 다수의 x-cdn 헤더가 포함되어 있으면 모든 헤더가 x-cdn: value1로 통합됩니다. |
| 삭제     | 지정된 응답 헤더의 매개변수를 삭제합니다.                                       |

> !
> - 일부 헤더는 자동 설정/삭제를 지원하지 않습니다. 상세 리스트는 [주의사항](#noice)을 참고하십시오.
> - HTTP 응답 헤더 설정 규칙은 최대 10개까지 설정할 수 있습니다.
> - 여러 규칙 간의 우선순위 조정 지원: 하단의 우선순위가 상단보다 높습니다. 하나의 헤더 매개변수에 여러 규칙이 설정되어 있는 경우에는 최하단 규칙, 즉 우선순위가 가장 높은 규칙이 적용됩니다.

### 헤더 매개변수

<table>
<thead>
<tr>
<th style="width:230px">헤더 매개변수</th>
<th>설명</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>리소스의 크로스 도메인 권한 문제를 해결하는 데 사용됩니다. 도메인 값은 해당 리소스에 액세스할 수 있는 도메인을 정의합니다. 출처를 요청한 Host가 도메인 설정 리스트에 있는 경우, 해당 값이 반환 헤더에 입력됩니다. 모든 도메인의 요청을 허용하도록 와일드카드 부호 ‘*’를 설정할 수도 있습니다. 자세한 내용은 <a href="#acao">Access-Control-Allow-Origin 매칭 모드 소개를 참고하십시오.</a> </br>'*' 입력 또는 다수의 도메인/IP/도메인 및 IP 혼합 입력이 가능합니다(반드시 <code>http://</code> 또는 <code>https://</code>를 포함해야 함, 입력 예시: <code>http://test.com,http://1.1.1.1</code>, 쉼표로 구분)(주의: 입력창에 최대 1000자까지 입력 가능). </td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>크로스 도메인에서 허용되는 HTTP 요청 방법을 설정하는 데 사용되며, 다음과 같이 여러 방법을 동시에 설정할 수 있습니다. <br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>. </td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>사전 요청의 유효 시간을 지정하는 데 사용되며, 단위는 초입니다. <br>비 단순 크로스 도메인 요청의 경우, 정식 통신 전에 크로스 도메인 요청이 안전하고 수용 가능한지 확인하기 위해 ‘사전 요청’이라는 HTTP 쿼리 요청을 추가해야 합니다.<br>GET, HEAD 또는 POST 이외의 방식으로 요청하거나 POST를 사용하지만 요청 데이터 유형은 application / x-www-form-urlencoded, multipart / form-data, text / plain 이외의 유형(예: application / xml 또는 text / xml)인 경우, 비 단순 크로스 도메인 요청으로 간주됩니다. <br>사용자 정의 요청 헤더가 ‘Access-Control-Max-Age:<code>1728000</code>’인 경우 1728000초(20일) 내에 해당 리소스에 대한 크로스 도메인 액세스가 다른 사전 요청을 추가로 보내지 않음을 나타냅니다. </td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>응답의 일부로 클라이언트에 노출할 수 있는 헤더를 지정하는 데 사용합니다. <br>기본적으로 Cache-Control, Content-Language, Content-Type, Expires, Last-Modified, Pragma와 같은 6가지 헤더만 클라이언트에 노출 가능합니다. <br>다음 설정을 통해 클라이언트가 다른 헤더 정보에 액세스하도록 할 수 있습니다. 여러 헤더를 입력할 때는 ‘,’로 구분해야 합니다. 예: <code>Access-Control-Expose-Headers: Content-Length, X-My-Header</code>는 클라이언트가 Content-Length와 X-My-Header의 두 헤더 정보에 액세스할 수 있음을 나타냅니다. </td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>브라우저 다운로드를 활성화하고 기본 다운로드 파일명을 설정하는 데 사용됩니다.<br>서버가 클라이언트 브라우저에 파일을 전송할 때, TXT, JPG 등과 같이 브라우저에서 지원하는 파일 형식인 경우 기본적으로 브라우저에서 파일을 직접 열게 됩니다. 사용자 저장이라는 메시지를 표시해야 하는 경우, Content-Disposition 필드 구성을 통해 브라우저 기본 동작을 덮어쓸 수 있습니다. 일반적으로 구성은 다음과 같습니다. <br><code>Content-Disposition: attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>페이지에 사용되는 언어 코드를 정의합니다. 일반적으로 다음과 같이 설정합니다. <br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>사용자 정의</td>
<td>사용자 정의 헤더 추가 및 사용자 정의 key-value 설정을 지원합니다. <br>사용자 정의 헤더 매개변수: 알파벳 대소문자, 숫자 및 -로 구성되며, 길이는 1 - 100자 사이로 제한됩니다. <br>사용자 정의 헤더 값의 길이: 1~1,000자로, 중국어는 지원되지 않습니다. </td>
</tr>
</tbody></table>


### Access-Control-Allow-Origin 매칭 모드 소개[](id:acao)

| **매칭 모드**   | **도메인 값**                                                     | **설명**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 완전 매칭         | *                                                            | *로 설정할 경우, 다음 응답 헤더를 추가합니다. 'Access-Control-Allow-Origin:*' |
| 고정 매칭       |'http://cloud.tencent.com' 'https://cloud.tencent.com' 'http://www.b.com' | 출처가 'https://cloud.tencent.com'이고 리스트를 히트한 경우, 다음 응답 헤더를 추가합니다. 'Access-Control-Allow-Origin: https://cloud.tencent.com' <br/>출처가 'https://www.qq.com'이고 리스트를 히트하지 못한 경우, 응답에 변화가 없습니다. |
| 2단계 와일드카드 서브도메인 매칭 | 'https://*.tencent.com'                                       | 출처가 'https://cloud.tencent.com'이고 리스트를 히트한 경우, 다음 응답 헤더를 추가합니다. 'Access-Control-Allow-Origin: https://cloud.tencent.com' <br/>출처가 'https://cloud.qq.com'이고 리스트를 히트하지 못한 경우, 응답에 변화가 없습니다. |
| 포트 매칭       | 'https://cloud.tencent.com:8080'                             | 출처가 'https://cloud.tencent.com:8080'이고 리스트를 히트한 경우, 다음 응답 헤더를 추가합니다. 'Access-Control-Allow-Origin:https://cloud.tencent.com:8080'<br/>출처가 'https://cloud.tencent.com'이고 리스트를 히트하지 못한 경우, 응답에 변화가 없습니다. |

> ! 특수 포트가 있는 경우, 목록에 관련 정보를 입력해야 하며, 임의 포트 매칭은 지원하지 않으므로 반드시 지정해야 합니다.

### 주의 사항[](id:noice)

해당 기능은 다음 헤더를 지원하지 않으므로 적용할 수 없습니다.

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
