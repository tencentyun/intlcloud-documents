## 기능 설명
DELETE Bucket 요청은 지정 계정에서 버킷을 삭제하는 데 사용됩니다.
>!버킷 삭제 전, 버킷 내 데이터와 업로드를 완료하지 않은 파트 데이터가 전부 지워졌는지 확인하십시오. 아닐 경우, 버킷을 삭제할 수 없게 됩니다.

## 요청
### 요청 예제
```
DELETE / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
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
해당 응답 본문은 비어 있습니다.

### 오류 분석
다음은 해당 요청에 발생할 수 있는 일부 특수하지만 흔히 볼 수 있는 오류 상황입니다. COS 오류 코드와 관련하여 더 많은 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

|오류 코드|HTTP 상태 코드|설명|
|-------|------|------|
|BucketNotEmpty|409 Conflict|버킷은 비어 있지 않아 삭제할 수 없습니다|
|AccessDenied|403 Forbidden|버킷 삭제는 역시 서명을 포함해야 합니다. 접근 권한이 없는 버킷을 삭제하려 시도하면 해당 오류가 반환됩니다|
|NoSuchBucket|404 Not Found|존재하지 않는 버킷을 삭제하면 해당 오류가 반환됩니다|


## 실제 사례

### 요청
```
DELETE / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484708950;32557604950&q-key-time=1484708950;32557604950&q-header-list=host&q-url-param-list=&q-signature=2b27b72ad2540ff2dde341dc7579a66ee8cb2afc
```

### 응답
```
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZWRjNjBfOTgxZjRlXzZhYjlfMTg0
```

