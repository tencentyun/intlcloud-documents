## 기능 설명
PUT Bucket cors API 요청은 버킷의 CORS 권한을 설정하는 데 사용됩니다. XML 형식의 구성 파일을 전달하여 구성할 수 있으며, 파일 크기는 64KB로 제한됩니다. 기본 상황에서 버킷 소유자는 해당 API 사용 권한을 바로 갖게 되며, 버킷 소유자는 그 권한을 다른 사용자에게 부여할 수도 있습니다.

## 요청
요청 예시:

```
PUT /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

<XML file>
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청행

```
PUT /?cors HTTP/1.1
```

해당 API는 `PUT` 요청을 수신합니다.


### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 ‘공용 요청 헤더’) 섹션을 참조하십시오.

#### 비공통 헤더


해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체
요청 본문은 크로스 도메인 규칙입니다.
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
  <CORSRule>
    <ID>string</ID>
    <AllowedOrigin>string</AllowedOrigin>
    <AllowedMethod>string</AllowedMethod>
    <AllowedHeader>string</AllowedHeader>
    <MaxAgeSeconds>0</MaxAgeSeconds>
    <ExposeHeader>string</ExposeHeader>
  </CORSRule>
</CORSConfiguration>
```


구체적인 데이터 설명은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|---|---|---|---|---|
|CORSConfiguration|없음|CORS 구성의 모든 정보이며, 최대 100개의 CORSRule을 포함할 수 있습니다.|Container|예|

Container 노드 CORSConfiguration의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|---|---|---|---|
|CORSRule|CORSConfiguration|CORS 구성의 모든 정보이며, 최대 100개의 CORSRule을 포함할 수 있습니다.|Container|예|

Container 노드 CORSRule의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|---|---|---|---|---|
|ID|CORSConfiguration.CORSRule|구성 규칙의 ID, 선택 가능|string|예|
|AllowedOrigin|CORSConfiguration.CORSRule|허가된 접근 소스, 와일드카드 *를 지원합니다. 형식은 프로토콜://도메인 이름[:포트]입니다. 예: http://www.qq.com|strings|예|
|AllowedMethod|CORSConfiguration.CORSRule|허가된 HTTP 작업입니다. 열거형 값: GET, PUT, HEAD, POST, DELETE|strings|예|
|AllowedHeader|CORSConfiguration.CORSRule|OPTIONS 요청 발송 시 서버에 다음 요청은 어느 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지 알립니다. 와일드카드 *를 지원합니다. |strings|예|
|MaxAgeSeconds|CORSConfiguration.CORSRule|OPTIONS 요청 획득 결과의 유효 기간을 설정합니다.|integer|예|
|ExposeHeader|CORSConfiguration.CORSRule|브라우저가 수신할 수 있는 서버측의 사용자 지정 헤더 정보를 설정합니다.|strings|예|


## 응답
### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 사용하며, 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729 ‘공통 응답 헤더’) 섹션을 참조하십시오.

#### 고유의 응답 헤더


해당 요청 작업은 특별한 응답 헤더 정보가 없습니다.

### 응답 본문
해당 요청 응답 본문은 비어 있습니다.

### 오류 코드

|오류 코드|설명|HTTP 상태 코드|
|---|---|---|
|SignatureDoesNotMatch|제공하는 서명이 규칙에 부합하지 않을 경우, 해당 오류 코드를 반환합니다.|403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
|NoSuchBucket|추가하려는 규칙이 위치한 버킷이 존재하지 않으면 해당 오류 코드를 반환합니다.|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## 실제 사례

### 요청

```
PUT /?cors HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2017 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=cors&q-signature=8b9f05dabce2578f3a79d732386e7cbade9033e3
Content-Type: application/xml
Content-Length: 280

<CORSConfiguration>
    <CORSRule>
        <ID>1234</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
    </CORSRule>
</CORSConfiguration>
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 10 Mar 2017 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdiZWRfOWExZjRlXzQ2OWVfZGY0
```
