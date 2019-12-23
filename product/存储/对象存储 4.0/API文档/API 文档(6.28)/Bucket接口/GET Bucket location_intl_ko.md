## 기능 설명
GET Bucket location API는 버킷 소재 지역의 정보를 획득하는 데 사용됩니다. 해당 GET 작업은 location 매개변수를 사용하여 버킷 소재 지역을 반환하고, 버킷 소유자만 해당 API에 대한 작업 권한이 있습니다.

## 요청
### 요청 예제

```
GET /?location HTTP/1.1
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
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
응답 본문 반환 지역 정보입니다.

```
<?xml version="1.0" encoding="UTF-8" ?>
<LocationConstraint>cos.ap-beijing</LocationConstraint>
```

구체적인 데이터 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
LocationConstraint|없음|버킷 소재 지역. 열거형 값은 [지역과 접근 도메인 이름](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 예: ap-beijing, ap-hongkong, eu-frankfurt 등|string|예

### 오류 코드
해당 요청 작업은 특별 오류 정보가 없습니다. 일반적인 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 섹션을 참조하십시오.


## 실제 사례

### 요청

```
GET /?location HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484817522;32557713522&q-key-time=1484817522;32557713522&q-header-list=host&q-url-param-list=location&q-signature=ceb96fc929663dd4d2e6dc0aeb304cdde6761ed
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 92
Connection: keep-alive
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDg0NzlfNDYyMDRlXzM0OWFfZjFk

<LocationConstraint>cos.ap-beijing</LocationConstraint>
```
