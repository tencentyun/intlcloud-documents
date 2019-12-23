## 기능 설명
DELETE Bucket policy 요청은 버킷 권한 정책을 삭제하는 데 사용됩니다.

>!버킷 소유자만 해당 요청을 제시할 권한이 있습니다. 권한 정책이 존재하지 않으면 204 No Content가 반환됩니다.

## 요청

### 요청 예제

```shell
DELETE /?policy HTTP/1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Authorization: Auth String
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).

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

## 실제 사례

### 요청

```shell
DELETE /?policy HTTP/1.1
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814613;32557710613&q-key-time=1484814613;32557710613&q-header-list=host&q-url-param-list=policy&q-signature=57c9a3f67b786ddabd2c208641944ec7f9b02f98
```

### 응답

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu Jan 19 16:30:21 2017
Server: tencent-cos
x-cos-request-id: NTg4MDc5MWRfNDQyMDRlXzNiMDRfZTEw
```

