## 기능 설명
HEAD Object API 요청은 해당 객체의 메타 정보 데이터를 획득할 수 있으며, HEAD의 권한은 GET의 권한과 일치합니다.

### 버전

기본 상황에서 HEAD 작업은 현재 버전의 객체에서 메타데이터를 인덱스합니다. 각기 다른 버전에서 메타데이터를 인덱스할 경우, versionId 서브 리소스를 사용하십시오.

## 요청
요청 예시:
```
HEAD /<ObjectName> HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청행

```
HEAD /{ObjectName} HTTP/1.1
```

해당 API는 `HEAD` 요청을 수신합니다.


### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 ‘공용 요청 헤더’) 섹션을 참조하십시오.

#### 비공통 헤더

이름|유형|필수 여부|설명
---|---|---|---
If-Modified-Since|string|아니요|객체가 지정 시간 이후 수정되면 해당 객체의 메타 정보를 반환하고 아닐 경우, 304를 반환합니다.


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
|x-cos-meta- *|string|사용자 지정 meta|
|x-cos-object-type|string|객체가 추가 업로드될 수 있는지를 표시하는 데 사용됩니다. 열거형 값: normal 또는 appendable|
|x-cos-storage-class|string|객체의 스토리지 클래스입니다. 열거형 값: STANDARD,STANDARD_IA|
|x-cos-version-id|string|반환된 객체의 버전 ID입니다.|
|x-cos-server-side​-encryption|string|COS 관리 서버 암호화를 통해 객체를 저장한 경우, 응답은 이 헤더와 사용한 암호화 알고리즘 값 AES256을 포함합니다 |


### 응답 본문
해당 요청 응답 본문은 비어 있습니다.

## 실제 사례

### 요청

```
HEAD /123 HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2017 17:26:53 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213210;32557109210&q-key-time=1484213210;32557109210&q-header-list=host&q-url-param-list=&q-signature=ac61b8eb61964e7e6b935e89de163a479a25c210
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
Date: Thu, 12 Jan 2017 17:26:53 GMT
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Last-Modified: Wed, 11 Jan 2017 07:30:07 GMT
Server: tencent-cos
x-cos-object-type: normal
x-cos-request-id: NTg3NzRiZGRfYmRjMzVfM2Y2OF81N2YzNA==
x-cos-storage-class: STANDARD
```
