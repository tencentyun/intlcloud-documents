## 기능 설명
DELETE Bucket cors API 요청은 CORS의 구성 정보 삭제를 구현합니다.

## 요청
### 요청 예제

```
DELETE /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String, 세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.

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

해당 응답은 공통 응답 헤더를 사용하며, 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729 "공통 응답 헤더") 섹션을 참조하십시오.

#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
해당 응답 본문은 비어 있습니다.

### 오류 코드
해당 요청 작업은 아래 오류 정보를 반환합니다. 일반적인 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 섹션을 참조하십시오.

오류 코드|설명|HTTP 상태 코드
---|---|---
None|삭제 성공, 응답 본문이 비어 있음|204 [No Content](https://tools.ietf.org/html/rfc7231#section-6.3.5)
NoSuchBucket|접근된 Bucket이 존재하지 않을 때, 해당 오류 코드를 반환합니다|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## 실제 사례

### 요청

```
DELETE /?lifecycle HTTP/1.1
Host:lifecycletest-73196696.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:59:09 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502859472;1502939472&q-key-time=1502859472;1502939472&q-header-list=host&q-url-param-list=lifecycle&q-signature=49c1414c700643f11139219384332a3ec4e9485b
```

### 응답

```
HTTP/1.1 204 No Content
Content-Type: application/xml
Date: Wed, 16 Aug 2017 12:59:09 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDQxOWNfMjQ4OGY3Xzc3NGRfMjE=
```
