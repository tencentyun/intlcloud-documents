## 기능 설명
GET Object API 요청은 COS의 버킷에서 하나의 파일(객체)을 로컬에 다운로드할 수 있습니다. 해당 작업은 요청자가 대상 객체에 대해 읽기 권한을 보유하거나 대상 객체가 모든 사용자에게 읽기 권한이 있습니다(공개 읽기).

### 버전
여러 버전을 시작할 때, 해당 GET 작업은 객체의 현재 버전을 반환합니다. 다른 버전을 반환하려면 versionId 매개 변수를 사용하십시오.

>**주의**
해당 객체의 현재 버전이 삭제 표기이면, COS의 행위는 해당 객체가 존재하지 않음을 표시하고 x-cos-delete-marker: true 응답을 반환합니다.

## 요청

요청 예시:
```
GET /<ObjectName> HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청행

```
GET /{ObjectName} HTTP/1.1
```

해당 API는 `GET` 요청을 수신합니다.

#### 요청 매개변수


| 이름                         | 유형   | 필수 선택 여부 | 설명                                      |
| ---------------------------- | ------ | ---- | ----------------------------------------- |
| response-content-type        | string | 아니요   | 응답 헤더 중 Content-Type 매개변수를 설정합니다.        |
| response-content-language    | string | 아니요   | 응답 헤더 중 Content-Language 매개변수를 설정합니다.    |
| response-expires             | string | 아니요   | 응답 헤더 중 Content-Expires 매개변수를 설정합니다.     |
| response-cache-control       | string | 아니요   | 응답 헤더 중 Cache-Control 매개변수를 설정합니다.       |
| response-content-disposition | string | 아니요   | 응답 헤더 중 Content-Disposition 매개변수를 설정합니다. |
| response-content-encoding    | string | 아니요   | 응답 헤더 중 Content-Encoding 매개변수를 설정합니다.    |

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 ‘공용 요청 헤더’) 섹션을 참조하십시오.

#### 비공통 헤더

| 이름                | 유형   | 필수 선택 여부 | 설명                                                         |
| ------------------- | ------ | ---- | ------------------------------------------------------------ |
| Range               | string | 아니요   | RFC 2616에서 정의한 지정 파일 다운로드 범위, 단위는 바이트(bytes)입니다.     |
| If-Unmodified-Since | string | 아니요   | 파일 수정 시간이 지정 시간보다 이르거나 같을 경우에만 파일 내용을 반환합니다. 그렇지 않을 경우 412(precondition failed)를 반환합니다. |
| If-Modified-Since   | string | 아니요   | 객체가 지정 시간 이후 수정될 경우, 해당 객체 메타 정보를 반환하고 아닐 경우, 304(not modified)를 반환합니다. |
| If-Match            | string | 아니요   | ETag가 지정된 내용과 일치해야 파일을 반환합니다. 그렇지 않을 경우, 412(precondition failed)를 반환합니다. |
| If-None-Match       | string | 아니요   | ETag가 지정 내용과 불일치해야 파일을 반환합니다. 그렇지 않을 경우, 304(not modified)를 반환합니다. |

### 요청체

해당 요청 본문이 비어 있습니다.

## 응답

### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 사용하며, 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729 "공통 응답 헤더") 섹션을 참조하십시오.

#### 고유의 응답 헤더

해당 요청 작업의 응답 헤더의 구체적인 데이터는 다음과 같습니다.

|이름|유형|설명|
|---|---|---|
|x-cos-meta- *|string|사용자 지정 메타데이터|
|x-cos-object-type|string|객체가 추가 업로드될 수 있는지를 표시하는 데 사용됩니다. 열거형 값: normal 또는 appendable|
|x-cos-storage-class|string|객체의 스토리지 클래스 열거형 값: STANDARD, STANDARD_IA|
|X-cos-version-id|string|검색된 객체가 유일한 버전의 ID를 보유하면 버전 ID를 반환합니다.|
|x-cos-server-side​-encryption|string|COS 관리 서버 암호화를 통해 객체를 저장한 경우, 응답은 이 헤더와 사용한 암호화 알고리즘의 값 AES256을 포함합니다.|


### 응답 본문

다운로드에 성공하였고 파일 내용은 응답 본문에 있습니다.

### 오류 코드

| 오류 코드                | 설명                               | HHTP 상태 코드                                                  |
| --------------------- | ---------------------------------- | ------------------------------------------------------------ |
| InvalidArgument       | 제공하는 매개변수 오류                     | 400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) |
|SignatureDoesNotMatch|제공하는 서명이 규칙에 부합하지 않을 경우, 해당 오류 코드를 반환합니다 |403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchKey             | 다운로드 파일이 존재하지 않을 경우, 해당 오류 코드를 반환합니다 | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## 실제 사례

### 요청1

```
GET /123 HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639
```

### 응답1

```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/octet-stream
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename=\"filename.jpg\"
Content-Range: bytes 0-16086/16087
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==
x-cos-storage-class: STANDARD

[Object]
```

### 요청2

**response-xxx 매개변수 휴대**

```
GET /123?response-content-type=application%2fxml HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484212200;32557108200&q-key-time=1484212200;32557108200&q-header-list=host&q-url-param-list=&q-signature=11522aa3346819b7e5e841507d5b7f156f34e639

```

### 응답2

```
HTTP/1.1 200 OK
Date: Wed, 28 Oct 2014 22:32:00 GMT
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
Accept-Ranges: bytes
Content-Disposition: attachment; filename=\"filename.jpg\"
Content-Range: bytes 0-16086/16087
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 28 Oct 2014 20:30:00 GMT
x-cos-object-type: normal
x-cos-request-id: NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ==
x-cos-storage-class: STANDARD

[Object]
```
