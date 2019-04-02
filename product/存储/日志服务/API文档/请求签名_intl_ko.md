## 준비 작업

1. SecretID와 SecretKey 획득
    콘솔의 [클라우드 API 키](https://console.cloud.tencent.com/capi) 페이지에서 획득할 수 있습니다.
2. 개발 언어 지정:
     지원되는 언어는 Java, PHP, C Sharp, C++, Node.js 및 Python을 포함되어 이에 제한되지 않습니다. 개발 언어에 따라 HMAC-SHA1 함수를 지정해야 합니다.

## 서명 내용
API를 통해 CLS로 시작된 HTTP 서명 요청은 다음 예시와 같이 표준 HTTP Authorization 헤더를 사용하여 전달됩니다.

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-type;host&q-url-param-list=logset_name&q-signature=e8b23b818caf4e33f196f895218bdabdbd1f1423
```

요청의 Host 필드는 `${region}.cls.myqcloud.com`이고 region 필드는 CLS 영역입니다. 베이징 지역의 경우 ap-beijing을 입력합니다. 전체 지역 리스트 형식은 [지역 리스트](https://cloud.tencent.com/document/product/614/18940)를 참조하십시오.

```
ap-beijing - 베이징
ap-shanghai - 상하이
ap-guangzhou - 광저우
ap-chengdu - 청두
```

여기서 서명 내용은 여러 개의 키-값 쌍으로 이루어지며, '&'를 통해 연결됩니다. 형식은 다음과 같습니다.

```shell
q-sign-algorithm=[Algorithm]&q-ak=[SecretId]&q-sign-time=[SignTime]&q-key-time=[KeyTime]&q-header-list=[SignedHeaderList]&q-url-param-list=[SignedParamList]&q-signature=[Signature]
```

### 키 값 설명

서명 내용을 구성하는 키-값(Key=Value) 설명은 다음과 같습니다.

<table>
   <tr>
      <th>키(Key)</th>
      <th>값(Value)</th>
      <th>의미</th>
   </tr>
   <tr>
      <td nowrap="nowrap">q-sign-algorithm</td>
      <td>sha1</td>
      <td>필수, 서명 알고리즘, 현재 sha1 만 지원</td>
   </tr>
   <tr>
      <td>q-ak</td>
      <td>매개변수[SecretId]</td>
      <td>필수, 계정의 SecretId, 위의 준비 작업에 콘솔에서 가져온 ID</td>
   </tr>
   <tr>
      <td>q-sign-time</td>
      <td>매개변수[SignTime]</td>
      <td>필수, 서명 유효 시작/종료 시간, Unix 타임스탬프, 단위: 초, 세미콜론으로 구분</td>
   </tr>
   <tr>
      <td>q-key-time</td>
      <td>매개변수[KeyTime]</td>
      <td>필수, q-sign-time 값과 같음</td>
   </tr>
   <tr>
      <td>q-header-list</td>
      <td>매개변수[SignedHeaderList]</td>
      <td>필수, 서명을 추가해야 하는 Http 요청 해더의 key입니다. key는 소문자로 전환해야 하고 여러 개의 키는 사전순으로 정렬되어야 하며 세미콜론으로 구분해야 합니다. 모든 header에 서명하지 않을 경우, 빈 문자열을 입력할 수 있습니다.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">q-url-param-list</td>
      <td>매개변수[SignedParamList]</td>
      <td>필수, 서명을 추가해야 하는 Http 요청 Uri의 일부 매개변수입니다. key는 소문자로 전환해야 하고 여러 개의 키는 사전순으로 정렬되어야 하며 세미콜론으로 구분해야 합니다. 모든 param에 서명하지 않을 경우, 빈 문자열을 입력할 수 있습니다.</td>
   </tr>
   <tr>
      <td>q-signature</td>
      <td>매개변수[Signature]</td>
      <td>필수, 계산된 서명 내용, 소문자</td>
   </tr>
</table>


>!q-sign-time 및 q-key-time의 경우 종료 시간이 시작 시간보다 늦어야 합니다. 그렇지 않으면 서명이 즉시 만료됩니다.

### 계산 방법

서명 계산 절차:

1. 특정 형식에 따라 HTTP 요청의 관련 정보를 HttpRequestInfo 문자열에 합칩니다.
2. sha1 알고리즘을 사용하여 HttpRequestInfo의 해시 값을 계산한 다음 해시 값을 특정 형식에 따라 다른 지정된 매개변수와 결합하여 서명 원문 문자열 StringToSign을 생성합니다.
3. SecretKey를 사용하여 q-key-time을 암호화하여 SignKey를 얻습니다.
4. SignKey를 사용하여 StringToSign을 암호화하여 Signature를 생성합니다.

>!특수 문자의 urlencode 결과는 대문자를 사용해야 합니다. 예를 들어, `/`는 `%2f`가 아니라 `%2F`로 인코딩되어야 합니다.

#### HttpRequestInfo 합치기

HttpRequestInfo는 아래와 같이 HTTP 요청의 Method, Uri, Headers 및 Parameters로 구성됩니다.
```
HttpRequestInfo = Method + "\n"
                + Uri + "\n"
                + FormatedParameters + "\n"
                + FormatedHeaders + "\n"
```

위의 `\n`은 줄 바꿈 이스케이프 문자이고 `+`는 문자열 연결 작업이며 다른 매개변수는 다음과 같이 정의됩니다.

| 필드 이름                | 의미                                       |
| ------------------ | ---------------------------------------- |
| Method             | HTTP 요청에 사용되는 메소드, 소문자, 예: `get, post` 등       |
| Uri                | HTTP 요청의 리소스 이름, query string를 포함하지 않습니다. 예: `/logset` |
| FormatedParameters | HTTP 요청 query string의 직렬화된 매개변수의 문자열, 즉 q-url-param-list에 지정된 매개변수. 지정하지 않으면 빈 문자열이 사용됩니다. key 및 value는 `=`로 연결하고 다른 키 값 쌍은 `&`로 연결되어 사전순으로 정렬되어야 하며 key는 소문자이고 value는 URL 인코딩해야 합니다. |
| FormatedHeaders    | HTTP 요청의 header, 즉 q-header-list에서 지정한 HTTP 헤더. 지정하지 않은 경우, 빈 문자열을 사용하고 key 및 value는 `=`로 연결하고 다른 키 값 쌍은 `&`로 연결되어 사전순으로 정렬되어야 하며 key는 소문자이고 value는 URL 인코딩해야 합니다. |

#### StringToSign 합치기

StringToSign은 아래와 같이 q-sign-algorithm, q-sign-time 및 HttpRequestInfo의 sha1 해시 값으로 구성됩니다.
```
StringToSign = q-sign-algorithm + "\n"
             + q-sign-time + "\n"
             + sha1(HttpRequestInfo) + "\n"
```

위의 `\n`은 줄 바꿈 이스케이프 문자이고 `+`는 문자열 연결 작업이며 다른 매개변수는 위에서 이미 설명하였습니다. 그 중 HttpRequestInfo의 sha1 해시 값은 16진수 소문자 문자열입니다.

#### SignKey 생성하기
현재 API는 하나의 디지털 서명 알고리즘인 hmac-sha1(기본값)만 지원합니다. 의사 코드는 다음과 같습니다.
```
SignKey = Hexdigest(HMAC-SHA1(q-key-time, SecretKey))
```

`HMAC-SHA1`은 암호화 알고리즘이며 `Hexdigest`는 16진수 문자열 전환에 사용되는 방법입니다. 암호화 알고리즘을 사용하는 일부 언어의 출력 결과는 16진수 문자열이므로 전환할 필요가 없습니다.

#### 서명 생성하기
현재 API는 하나의 디지털 서명 알고리즘인 hmac-sha1(기본값)만 지원합니다. 의사 코드는 다음과 같습니다.
```
Signature = Hexdigest(HMAC-SHA1(StringToSign, SignKey))
```

`HMAC-SHA1`은 암호화 알고리즘이며 `Hexdigest`는 16진수 문자열 전환에 사용되는 방법입니다. 암호화 알고리즘을 사용하는 일부 언어의 출력 결과는 16진수 문자열이므로 전환할 필요가 없습니다.

## 예시

다음 SecretId 및 SecretKey를 예로 들어봅니다.

```
SecretId = "AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX"
SecretKey = "LUSE4nPK1d4tX5SHyXv6tZXXXXXXXXXX"

StartTime = 1510109254
EndTime = 1510109314
```

**예시 1**:
logset 정보를 얻으려면 HTTP 요청은 다음과 같습니다.
```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
```

위 요청의 경우 요청 헤더 Host에 서명이 추가되면 생성된 HttpRequestInfo 문자열은 다음과 같습니다.

```
get\n/logset\nlogset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\nhost=ap-shanghai.cls.myqcloud.com\n
```

HttpRequestInfo를 사용하여 생성된 서명 원문 문자열 StringToSign은 다음과 같습니다.

```
sha1\n1510109254;1510109314\n35601c3365a361b62b980fda754318c29862d39c\n
```

SecretKey를 사용하여 q-key-time을 암호화하여 SignKey를 얻습니다.

```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

SignKey를 사용하여 StringToSign을 암호화하여 Signature를 생성합니다.

```
2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

합치된 Authorization은 다음과 같습니다.

```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

최종 요청 내용은 다음과 같습니다.

```
GET /logset?logset_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=host&q-url-param-list=logset_id&q-signature=2c53900d3fe8d2e875db8a6af5fe7303ee1567a8
```

**예시 2**:
logset 정보를 수정하려면 HTTP 요청은 다음과 같습니다.
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-Length: 50

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```

본문 내용에 대해 계산된 md5 값은 다음과 같습니다.
```
f9c7fc33c7eab68dfa8a52508d1f4659
```

위 요청의 경우 요청 헤더 Host에 서명이 추가되면 생성된 HttpRequestInfo 문자열은 다음과 같습니다.
```
put\n/logset\n\ncontent-md5=f9c7fc33c7eab68dfa8a52508d1f4659&content-type=application%2Fjson&host=ap-shanghai.cls.myqcloud.com\n
```

HttpRequestInfo를 사용하여 생성된 서명 원문 문자열 StringToSign은 다음과 같습니다.
```
sha1\n1510109254;1510109314\n0ca0242c3d50441fda6aa234d31bea7a7a12a1ea\n
```

SecretKey를 사용하여 q-key-time을 암호화하여 SignKey를 얻습니다.
```
a4501294d3a835f8dab6caf5c19837dd19eef357
```

SignKey를 사용하여 StringToSign을 암호화하여 Signature를 생성합니다.
```
85a55e61de42483ba03bffd07a6c01b8d651af51
```

합치된 Authorization은 다음과 같습니다.
```
q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51
```

최종 요청 내용은 다음과 같습니다.
```
PUT /logset HTTP/1.1
Host: ap-shanghai.cls.myqcloud.com
Content-Type: application/json
Content-MD5: f9c7fc33c7eab68dfa8a52508d1f4659
Content-Length: 50
Authorization: q-sign-algorithm=sha1&q-ak=AKIDc9YlmrBcFk4C8sbmXQ8i65XXXXXXXXXX&q-sign-time=1510109254;1510109314&q-key-time=1510109254;1510109314&q-header-list=content-md5;content-type;host&q-url-param-list=&q-signature=85a55e61de42483ba03bffd07a6c01b8d651af51

{"logset_id":"xxxx-xx-xx-xx-xxxxxxxx","period":30}
```
