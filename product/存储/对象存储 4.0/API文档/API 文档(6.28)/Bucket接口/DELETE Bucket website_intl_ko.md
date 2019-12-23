## 기능 설명

DELETE Bucket website 요청은 버킷의 정적 웹사이트 구성을 삭제하는 데 사용됩니다.

## 요청

### 요청 예제

```HTTP
DELETE /?website HTTP/1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조).

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더

해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체

해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더

해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문

해당 응답 본문은 비어 있습니다.

### 오류 코드

해당 요청 작업은 특별한 오류 정보가 없습니다. 흔히 볼 수 있는 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청

```
DELETE /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date:Thu, 21 Sep 2017 13:21:09 +0000
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484816036;32557712036&q-key-time=1484816036;32557712036&q-header-list=host&q-url-param-list=website&q-signature=e92eecbf0022fe7e5fd39b2c500b22da062be50a
```

### 응답

```
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 21 Sep 2017 13:21:18 GMT
Server: tencent-cos
x-cos-request-id: NTljM2JjY2RfMjQ4OGY3MGFfNzk4OV84Mw==
```
