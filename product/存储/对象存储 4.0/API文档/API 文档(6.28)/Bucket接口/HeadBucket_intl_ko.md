## 기능 설명
HEAD Bucket 요청은 해당 버킷 존재 여부, 접근 권한 존재 여부를 확인할 수 있습니다. HEAD의 권한은 Read와 일치하며 다음 몇 가지 상황이 있습니다.
- 버킷이 존재할 경우, HTTP 상태 코드를 200으로 반환합니다.
- 버킷에 접근 권한이 없을 경우, HTTP 상태 코드를 403으로 반환합니다.
- 버킷이 존재하지 않을 경우, HTTP 상태 코드를 404로 반환합니다.

>!현재 버킷 속성을 획득하는 API(즉 acl 등 정보 반환 가능)를 공개하지 않았습니다.

## 요청
### 요청 예제

```shell
HEAD / HTTP/1.1
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

## 실제 사례

### 요청
```shell
HEAD / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 27 Oct 2015 20:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484640517;32557536517&q-key-time=1484640517;32557536517&q-header-list=host&q-url-param-list=&q-signature=7bedc2f84a0a3d29df85fe727d0c1e388c410376
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Thu, 27 Oct 2015 20:32:00 GMT
x-cos-request-id: NTg3ZGQxNDNfNDUyMDRlXzUyOWNfMjY5
```
