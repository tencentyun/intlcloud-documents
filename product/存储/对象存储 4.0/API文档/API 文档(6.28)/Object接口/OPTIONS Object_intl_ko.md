## 기능 설명
Options Object API는 CORS 구성의 사전 요청(Preflight)을 구현합니다. 즉, 크로스 도메인 요청을 보내기 전에 하나의 OPTIONS 요청을 보내고 COS에 특정 소스 도메인, HTTP 방식과 헤더 정보 등을 전달하고 크로스 도메인 요청을 보낼 수 있는지 여부를 결정합니다. CORS 구성이 존재하지 않을 경우, 요청은 403 Forbidden을 반환합니다. PUT Bucket cors API를 통하여 버킷에 CORS 지원을 활성화할 수 있습니다.

## 요청
### 요청 예제

```
OPTIONS /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Origin: Origin
Access-Control-Request-Method: HTTPMethod
Access-Control-Request-Headers: RequestHeader
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.).

### 요청 헤더
#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더

이름|유형|설명|필수 여부
---|---|---|---
Origin|string|CORS의 요청 소스 도메인 이름 시뮬레이션|예
Access-Control-Request-Method|string|CORS의 HTTP 요청 방식 시뮬레이션|예
Access-Control-Request-Headers|string|CORS의 요청 헤더 시뮬레이션|아니요

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답
### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.

#### 고유의 응답 헤더

해당 요청 작업의 특유 응답 헤더의 구체적인 데이터는 다음과 같습니다.

|이름|유형|설명|
|---|---|---|
|Access-Control-Allow-Origin|string|CORS의 요청 소스 도메인 이름 시뮬레이션, 소스가 허용되지 않았을 경우, 해당 헤더는 반환하지 않습니다.|
|Access-Control-Allow-Methods|string|CORS의 HTTP 요청 방식 시뮬레이션, 요청 방식이 허용되지 않았을 경우, 이 헤더는 반환하지 않습니다.|
|Access-Control-Allow-Headers|string|CORS의 요청 헤더 시뮬레이션, 임의 요청 헤더 시뮬레이션이 허용되지 않았을 경우, 이 헤더는 해당 요청 헤더를 반환하지 않습니다.|
|Access-Control-Expose-Headers|string|CORS의 HTTP 요청 방식 시뮬레이션, 요청 방식이 허용되지 않았을 경우, 이 헤더는 반환하지 않습니다.|
|Access-Control-Max-Age|string|OPTIONS 요청 획득 결과의 유효 기간을 설정합니다.|

### 응답 본문
해당 응답 본문은 비어 있습니다.

## 실제 사례

### 요청

```
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2017 17:26:53 GMT
Origin: http://www.qq.com
Access-Control-Request-Method: PUT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1487070734;32466654734&q-key-time=1487070734;32559966734&q-header-list=host&q-url-param-list=&q-signature=2ac3ada19910f44836ae0df72a0ec1003f34324b
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
x-cos-request-id: NTg3NzRiZGRfYmRjMzVfM2Y2OF81N2YzNA==
Date: Thu, 12 Jan 2017 17:26:53 GMT
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Access-Control-Allow-Origin: http://www.qq.com
Access-Control-Allow-Methods: PUT
Access-Control-Expose-Headers: x-cos-request-id
Server: tencent-cos
```
