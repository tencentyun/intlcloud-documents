## 기능 설명
Get Service API는 요청자 이름 하의 모든 스토리지 공간 리스트(Bucket list)를 획득하는 데 사용됩니다.

## 요청
### 요청 예제

```
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.).

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
해당 요청 작업은 특별한 응답 헤더 정보가 없습니다.

### 응답 본문
조회 성공, application/xml 데이터를 반환하며 Bucket의 개체 정보를 포함합니다.
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<ListAllMyBucketsResult>
  <Owner>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Owner>
  <Buckets>
    <Bucket>
      <Name>string</Name>
      <Location>string</Location>
      <CreateDate>string</CreateDate>
    </Bucket>
    <DisplayName>string</DisplayName>
  </Buckets>
</ListAllMyBucketsResult>
```

구체적인 데이터 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ListAllMyBucketsResult|없음|이번 응답의 모든 정보를 설명합니다.|Container|예

Container 노드 ListAllMyBucketsResult의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Owner|ListAllMyBucketsResult|Bucket 보유자 정보를 설명합니다.|Container|예
Buckets|ListAllMyBucketsResult|이번 응답의 모든 Bucket 리스트 정보를 설명합니다.|Container|예
Container 노드 Owner의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ID|ListAllMyBucketsResult.Owner|Bucket 보유자의 ID|string|예
DisplayName|ListAllMyBucketsResult.Owner|Bucket 보유자의 이름 정보|string|예
Container 노드 Buckets의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Bucket|ListAllMyBucketsResult.Buckets|단일 Bucket의 정보|Container|예
DisplayName|ListAllMyBucketsResult.Buckets|Bucket 보유자의 이름 정보|string|예
Container 노드 Bucket의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Name|ListAllMyBucketsResult.Buckets.Bucket|Bucket의 이름|string|예
Location|ListAllMyBucketsResult.Buckets.Bucket|Bucket 소재 지역을 설명합니다. 열거값은 [가용 영역](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 예: ap-beijing, ap-hongkong, eu-frankfurt 등|string|예
CreateDate|ListAllMyBucketsResult.Buckets.Bucket|Bucket 생성 시간이며 ISO8601 형식입니다. 예: 2016-11-09T08:46:32.000Z|string|예


### 오류 코드

오류 코드|설명|HTTP 상태 코드
---|---|---
InvalidBucketName|Bucket 이름이 잘못되었습니다.|400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)
SignatureDoesNotMatch|제공하는 서명이 규칙에 부합하지 않을 경우, 해당 오류 코드를 반환합니다.|403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)
NoSuchBucket|Bucket이 존재하지 않을 때, 해당 오류 코드를 반환합니다.|404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)


## 실제 사례

### 요청

```
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: Thu, 12 Jan 2016 19:12:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1489110340;32468694340&q-key-time=1489110340;32562006340&q-header-list=host&q-url-param-list=&q-signature=cb46d5ce6daed2d3dc0db7130a5719349760562
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 19935
Connection: keep-alive
Date: Thu, 12 Jan 2016 19:12:22 GMT
Server: tencent-cos
x-cos-request-id: NThjMjA1NGFfNTViMjM1XzI0NWRfMjA4OGIx

<ListAllMyBucketsResult>
    <Owner>
     <ID>qcs::cam::uin/1147518609:uin/1147518609</ID>
     <DisplayName>1147518609</DisplayName>
    </Owner>
    <Buckets>
        <Bucket>
            <Name>01</Name>
            <Location>ap-beijing</Location>
            <CreateDate>2016-09-13 15:20:15</CreateDate>
        </Bucket>
        <Bucket>
            <Name>0111</Name>
            <Location>ap-hongkong</Location>
            <CreateDate>2017-01-11 17:23:51</CreateDate>
        </Bucket>
        <Bucket>
            <Name>1201new</Name>
            <Location>eu-frankfurt</Location>
            <CreateDate>2016-12-01 09:45:02</CreateDate>
        </Bucket>
    </Buckets>
</ListAllMyBucketsResult
```



