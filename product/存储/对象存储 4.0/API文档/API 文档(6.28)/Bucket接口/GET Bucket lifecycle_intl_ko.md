## 기능 설명
GET Bucket lifecycle은 버킷의 수명 주기 구성을 조회하는 데 사용됩니다. 해당 버킷에 수명 주기 규칙이 구성되어 있지 않으면 NoSuchLifecycleConfiguration을 반환합니다.

## 요청
### 요청 예제

```shell
GET /?lifecycle HTTP/1.1
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
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.

#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
응답 본문 중 요소의 내용 및 함의는 PUT Buket lifecycle 시 요청 본문과 일치합니다. 세부 정보는 [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) 요청 본문 노드 설명 내용을 참조하십시오.

### 오류 코드
해당 요청 작업은 특별 오류 정보가 없습니다. 일반적인 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 섹션을 참조하십시오.

## 실제 사례

### 요청
```shell
GET /?lifecycle HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 12:23:54 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502857357;1502937357&q-key-time=1502857357;1502937357&q-header-list=host&q-url-param-list=lifecycle&q-signature=da155cda3461bee7422ee95367ac8013ef847e02

```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 312
Date: Wed, 16 Aug 2017 12:23:54 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDM5NWFfMjQ4OGY3Xzc3NGRfMjA=

<LifecycleConfiguration>
  <Rule>
    <ID>id1</ID>
    <Filter>
       <Prefix>documents/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>100</Days>
      <StorageClass>STANDARD_IA</StorageClass>
    </Transition>
  </Rule>
  <Rule>
    <ID>id2</ID>
    <Filter>
       <Prefix>logs/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Expiration>
      <Days>10</Days>
    </Expiration>
  </Rule>
</LifecycleConfiguration>
```
