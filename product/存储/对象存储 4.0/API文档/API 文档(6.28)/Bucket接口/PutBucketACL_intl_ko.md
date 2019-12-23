## 기능 설명
PUT Bucket acl API는 Bucket의 acl 테이블에 입력하는 데 사용됩니다. Header "x-cos-acl", "x-cos-grant-read", "x-cos-grant-full-control"을 통하여 acl 정보를 전달하거나 본문을 통해 XML 형식으로 acl 정보를 전달할 수 있습니다.

>!
>- Header와 Body 중 하나만 선택할 수 있으며 그렇지 않으면 반환 응답이 충돌될 수 있습니다.
>- PUT Bucket acl은 덮어쓰기 작업으로 새로운 acl을 전달하면 기존의 acl을 덮어쓰기하게 됩니다.
>- 버킷 생성자에게만 작업 권한이 있습니다.

### 세부 분석
1. 헤더를 통해 설정하거나 xml 본문을 통해 설정할 수 있습니다. 한 가지 방법만 사용하길 권장합니다.
2. 개인 버킷은 하나의 폴더를 공개로 설정할 수 있으며, 그럼 해당 폴더의 파일은 모두 공개됩니다. 단, 폴더를 개인으로 설정하면, 해당 폴더에 설정한 공개 속성은 적용되지 않습니다.

## 요청
### 요청 예제

```
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
>Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).


### 요청 헤더

**공통 헤더**
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

**비공용 헤더**
해당 요청 장업은 PUT 요청 중 x-cos-acl 헤더로 버킷 접근 권한을 설정하여 구현할 수 있습니다. 현재 버킷 접근 권한은 public-read-write, public-read와 private 세 가지가 있습니다. 설정하지 않을 경우, private 권한을 기본으로 하며 사용자의 읽기, 쓰기 또는 읽기/쓰기 권한을 단독으로 명확히 부여할 수 있습니다. 내용은 다음과 같습니다.

|이름|설명|유형|필수 선택 여부|
|:---|:-- |:--|:--|
| x-cos-acl | 버킷의 acl 속성을 정의합니다. 유효값: private, public-read-write, public-read. 기본값: private | String|  아니요 |
| x-cos-grant-read |권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id="[OwnerUin]" | String |  아니요 |
| x-cos-grant-write| 권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id="[OwnerUin]" |String |  아니요 |
| x-cos-grant-full-control | 권한을 부여받은 자에게 모든 권한을 부여합니다. 형식: x-cos-grant-full-control: id="[OwnerUin]" | String|  아니요 |

### 요청체
해당 요청 작업을 구현하면 요청 본문 중 특정 요청 매개 변수를 갖고 버킷 접근 권한을 설정할 수 있습니다. 단, 요청 본문이 매개변수를 갖는 방식과 요청 헤더가 acl 서브 리소스를 갖는 방식 중 하나만 선택할 수 있습니다.
모든 노드를 가진 요청 본문 예시:
```
<AccessControlPolicy>
  <Owner>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```
구체적인 데이터 내용은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:-- |:--|:--|:--|
| AccessControlPolicy |없음| GET Bucket acl 결과를 저장하는 컨테이너 | Container |예|

Container 노드 AccessControlPolicy의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:-- |:--|:--|:--|
| Owner | AccessControlPolicy | 버킷 소유자 정보 |  Container |예|
| AccessControlList | AccessControlPolicy | 권한을 부여받은 자의 정보와 권한 정보 |  Container |예|

Container 노드 Owner의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:-- |:--|:--|:--|
| ID | AccessControlPolicy.Owner | 버킷 소유자의 ID, </br>형식: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; 루트 계정일 경우, &lt;OwnerUin&gt;와 &lt;SubUin&gt;은 동일 값입니다. |  String |예|

Container 노드 AccessControlList의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grant | AccessControlPolicy.AccessControlList | 단일 버킷의 권한 정보입니다. 1개 AccessControlList는 100개의 Grant를 보유할 수 있습니다. | Container    |예|

Container 노드 Grant의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 리소스 정보입니다. type 유형은 RootAccount, SubAccount일 수 있습니다. </br>type 유형이 RootAccount일 경우, uin에 QQ를 입력하거나, ID 중 uin에 QQ를 입력할 수 있으며, anyone(모든 유형 사용자를 의미)으로 uin/&lt;OwnerUin&gt;와 uin/&lt;SubUin&gt;를 대체할 수 있습니다.</br>type 유형이 RootAccount일 경우, uin은 루트 계정을 의미하고 Subaccount는 서브 계정을 의미합니다. | Container    |예|
| Permission | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 권한 정보를 명확히 합니다. 열거형 값: READ, WRITE, FULL_CONTROL  | String    |예|

Container 노드 Grantee의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | 사용자의 ID, </br>형식: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; 루트 계정일 경우, &lt;OwnerUin&gt;와 &lt;SubUin&gt;는 동일 값입니다. |  String |예|


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

|오류 코드|설명|HTTP 상태 코드|
|------|------|------|
|InvalidDigest|400 Bad Request|사용자가 보유한 Content-MD5와 COS 계산 본문의 Content-MD5는 일치하지 않습니다.|
|MalformedXM|400 Bad Request|전달한 xml 형식에 오류가 있습니다. restful api 문서와 자세히 비교하십시오.|
|InvalidArgument|400 Bad Request|매개변수 오류, 구체적인 내용은 오류 정보를 참조하십시오.|

## 실제 사례

### 요청
```
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

<AccessControlPolicy>
  <Owner>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee>
      <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

### 응답
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw

```
