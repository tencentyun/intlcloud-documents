## 기능 설명
GET Bucket cors API는 버킷 소유자가 버킷에 CORS의 정보 구성 획득을 구현합니다(cors는 W3C 표준으로 전체 이름은 "크로스 도메인 리소스 공유"(Cross-origin resource sharing)임). 기본적으로 버킷의 소유자는 해당 API에 대한 사용 권한이 있으며, 버킷 소유자는 권한을 다른 사용자에게 부여할 수도 있습니다.

## 요청
### 요청 예제

```
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.
#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답 패킷은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
CORS의 정보 구성 획득에 성공했습니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```

구체적인 데이터 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
CORSConfiguration|없음|CORS 구성의 모든 정보이며, 최대 100개의 CORSRule을 포함할 수 있습니다|Container|예

Container 노드 CORSConfiguration의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
CORSRule|CORSConfiguration|CORS 구성의 모든 정보이며, 최대 100개의 CORSRule을 포함할 수 있습니다|Container|예

Container 노드 CORSRule의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ID|CORSConfiguration.CORSRule|구성 규칙의 ID, 선택 가능|string|예
AllowedOrigin|CORSConfiguration.CORSRule|허가된 접근 소스로 와일드카드`*`를 지원하며, 형식은 프로토콜://도메인 이름[:포트]입니다. 예: `http://www.qq.com`|strings|예
AllowedMethod|CORSConfiguration.CORSRule|허가된 HTTP 작업, 열거형 값: GET, PUT, HEAD, POST, DELETE|strings|예
AllowedHeader|CORSConfiguration.CORSRule|OPTIONS 요청을 발송할 때 서버에 다음 요청은 어느 사용자 지정의 HTTP 요청 헤더를 사용할 수 있는지 알립니다. 와일드카드*를 지원합니다 |strings|예
MaxAgeSeconds|CORSConfiguration.CORSRule|OPTIONS 요청으로 획득하는 결과의 유효 기간을 설정합니다|integer|예
ExposeHeader|CORSConfiguration.CORSRule|브라우저가 수신할 수 있는 서버에서 온 사용자 지정 헤더 정보를 설정합니다|strings|예


### 오류 코드
해당 요청 작업은 특별 오류 정보가 없습니다. 일반적인 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 섹션을 참조하십시오.

## 실제 사례

### 요청

```
GET /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=cors&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 345
Connection: keep-alive
Date: Wed, 28 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFfZTBh

<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```
