## 기능 설명

DELETE Object API 요청은 COS의 버킷에서 하나의 파일(Object)을 삭제할 수 있습니다. 해당 작업은 요청자가 버킷에 대한 쓰기 권한이 있어야 합니다.

### 세부 분석

- DELETE Object 요청에서 존재하지 않는 객체를 삭제하여도 여전히 성공한 것으로 간주하며 `204 No Content`를 반환합니다.
- DELETE Object를 사용하려면 사용자가 해당 객체에 대한 쓰기 권한이 있어야 합니다.

## 요청

### 요청 예제
```shell
DELETE /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](/document/product/436/7778) 문서를 참조).

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더

해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.


### 요청체

해당 요청의 요청 본문은 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더 

해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.
#### 고유의 응답 헤더

해당 요청은 특별한 요청 헤더가 없습니다.

### 응답 본문

해당 요청의 응답 본문은 비어 있습니다.

### 오류 분석

다음은 이 요청이 일으킬 수 있는 특별하지만 흔히 볼 수 있는 오류 상황을 설명합니다.

|오류 코드|HTTP 상태 코드|설명|
|--|--|--|
| NoSuchBucket |404 Not Found|버킷이 존재하지 않습니다.| 

COS 오류 코드에 대한 세부 정보 또는 제품의 모든 오류 리스트는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.
## 실제 사례

### 요청
```shell
DELETE /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213409;32557109409&q-key-time=1484213409;32557109409&q-header-list=host&q-url-param-list=&q-signature=1c24fe260ffe79b8603f932c4e916a6cbb0af44a
```

### 응답
```shell
HTTP /1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjYTRfYmRjMzVfMzFhOF82MmM3Yg==
```

