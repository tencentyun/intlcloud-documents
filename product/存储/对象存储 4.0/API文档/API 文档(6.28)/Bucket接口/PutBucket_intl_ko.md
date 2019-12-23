## 기능 설명
PUT Bucket API 요청은 지정 계정에서 버킷 하나를 생성할 수 있습니다. 해당 API는 익명의 요청을 지원하지 않으므로 Authorization 서명 인증을 보유한 요청을 사용해야 새로운 버킷을 생성할 수 있습니다. 버킷을 생성한 사용자는 기본적으로 버킷 소유자가 됩니다.
### 세부 분석
1. 버킷 생성 시, 접근 권한을 지정하지 않으면 기본적으로 비공개 읽기/쓰기(private) 권한을 사용하게 됩니다.

## 요청

구문 예시:
```
PUT / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청행
~~~
PUT/HTTP/1.1
~~~
해당 API는 PUT 요청을 수신합니다.

### 요청 헤더

**공통 헤더**
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

**비공통 헤더**
해당 요청 장업은 PUT 요청 중 x-cos-acl 헤더로 버킷 접근 권한을 설정하여 구현할 수 있습니다. 현재 버킷 접근 권한은 public-read-write, public-read와 private 세 가지가 있습니다. 설정하지 않을 경우, private 권한을 기본으로 하며 사용자의 읽기, 쓰기 또는 읽기/쓰기 권한을 단독으로 명확히 부여할 수 있습니다. 내용은 다음과 같습니다.
>acl 요청에 대한 세부 정보는 [Put Bucket ACL](https://cloud.tencent.com/document/product/436/7737) 문서를 참조하십시오.

|이름|설명|유형|필수 선택 여부|
|:---|:-- |:--|:--|
| x-cos-acl | Object의 acl 속성을 정의합니다. 유효값: private, public-read-write, public-read. 기본값: private | String|  아니요 |
| x-cos-grant-read | 권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id=" ",id=" ". <br/>서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br/>루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" | String |  아니요 |
| x-cos-grant-write | 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id=" ",id=" ". <br/>서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br/>루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" |String |  아니요 |
| x-cos-grant-full-control | 권한을 부여받은 자에게 읽기/쓰기 권한을 부여합니다. 형식: x-cos-grant-full-control: id=" ",id=" ". <br/>서브 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br/>루트 계정에 권한을 부여해야 할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" | String|  아니요 |

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.
### 응답 본문
해당 응답 본문 반환이 비어 있습니다.
### 오류 분석
다음은 이 요청이 일으킬 수 있는 특별하지만 흔히 볼 수 있는 오류 상황을 설명합니다.

|오류 코드|HTTP 상태 코드|설명|
|--------|--------|--------------|
| BucketAlreadyExists |409 Conflict|요청이 생성한 버킷이 이미 존재하고, 생성을 요청한 사용자가 바로 소유자입니다.|
| InvalidBucketName | 400 Bad Request|버킷 이름은 규칙에 부합하지 않습니다. 구체적인 이유는 message 설명을 참조하십시오.|
| InvalidRequest | 400 Bad Request|버킷 이름은 규칙에 부합하지 않습니다. 구체적인 이유는 message 설명을 참조하십시오.|
버킷에 설정한 ACL이 정확하지 않으면 버킷 생성 실패를 초래할 수 있고 동시에 "Failed to set access control authority for the bucket" 오류 정보를 반환합니다. 구체적인 오류 원인은 반환한 오류 코드를 기반으로 [Put Bucket ACL](https://cloud.tencent.com/document/product/436/7737) 관련 문서를 참조하십시오.

COS 오류 코드에 대한 세부 정보 또는 제품의 모든 오류 리스트는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청
```
PUT / HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2016 19:12:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484708728;32557604728&q-key-time=1484708728;32557604728&q-header-list=host&q-url-param-list=&q-signature=b394a86624cbcc705b11bc6fc505843c5e2dd9c9
```

### 응답
```
HTTP /1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 12 Jan 2016 19:12:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZWRiODJfOWIxZjRlXzZmNDBfMTUz

```
