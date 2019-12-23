## 기능 설명
PUT Object acl API는 Bucket의 Object에 ACL 테이블을 구성하는 데 사용되며, Header:"x-cos-acl", "x-cos-grant-read", "x-cos-grant-full-control"을 통해 ACL 정보를 전달하거나 Body를 통해 XML 형식으로 ACL 정보를 전달할 수 있습니다.

## 요청
### 요청 예제

```shell
PUT /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 "공통 요청 헤더") 문서를 참조하십시오.

#### 비공통 헤더

<table>
   <tr>
      <th>이름</th>
      <th>설명</th>
      <th>유형</th>
      <th>필수 여부</th>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-acl</td>
      <td>Object의 ACL 속성을 정의합니다. 유효값은 private, public-read, default이며, 기본값은 default(버킷 권한 승계)입니다. <br>주의: 현재 접근 정책 항목은 1000개로 제한됩니다. Object ACL 제어를 진행할 필요가 없다면, default를 입력하거나 이 항목을 설정하지 마십시오. 버킷 권한 승계을 기본으로 합니다.</td>
      <td>string</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-read</td>
      <td>권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id="[OwnerUin]"</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-full-control</td>
      <td>권한을 부여받은 자에게 권한을 부여합니다. 형식: x-cos-grant-full-control: id="[OwnerUin]"</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
</table>


### 요청체
해당 요청의 요청체는 ACL 구성 규칙입니다.
```shell
<AccessControlPolicy>
   <Owner>
     <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
     <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
   </Owner>
   <AccessControlList>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
           <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
        </Grantee>
        <Permission>READ</Permission>
     </Grant>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
           <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
           <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
        </Grantee>
        <Permission>FULL_CONTROL</Permission>
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
|DisplayName	|AccessControlPolicy.Owner |Bucket 소유자의 이름 정보	|string	|예|

Container 노드 AccessControlList의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grant | AccessControlPolicy.AccessControlList | 단일 버킷의 권한 정보입니다. 1개 AccessControlList는 100개의 Grant를 보유할 수 있습니다. | Container    |예|

Container 노드 Grant의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 리소스 정보입니다. type 유형은 RootAccount, SubAccount일 수 있습니다. </br>type 유형이 RootAccount일 경우, uin에 QQ를 입력하거나, ID 중 uin에 QQ를 입력할 수 있으며, anyone(모든 유형 사용자를 의미)으로 uin/&lt;OwnerUin&gt;와 uin/&lt;SubUin&gt;를 대체할 수 있습니다.</br>type 유형이 RootAccount일 경우, uin은 루트 계정을 의미하고 Subaccount는 서브 계정을 의미합니다. | Container    |예|
| Permission | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 권한 정보를 명확히 합니다. 열거값: READ, FULL_CONTROL  | String    |예|

Container 노드 Grantee의 내용:

| 노드이름(키워드)          |부모 노드 | 설명                                    | 유형        |필수 여부|
| ------------ | ------------------------------------- | --------- |:--|:--|
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | 사용자의 ID, </br>형식: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; 루트 계정일 경우, &lt;OwnerUin&gt;와 &lt;SubUin&gt;는 동일 값입니다. |  String |예|
|DisplayName|AccessControlPolicy.AccessControlList.Grant.Grantee |Bucket 소유자의 이름 정보|string	|예|


## 응답
### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729 "공통 응답 헤더") 문서를 참조하십시오.

#### 고유의 응답 헤더
해당 요청 작업은 특별한 응답 헤더 정보가 없습니다.

### 응답 본문
해당 요청 응답 본문은 비어 있습니다.

### 오류 코드
해당 응답은 다음 오류 코드 정보가 나타날 수 있으며, 흔히 볼 수 있는 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

<table>
   <tr>
      <th>오류 코드</th>
      <th>설명</th>
      <th>HTTP 상태 코드</th>
   </tr>
   <tr>
      <td>SignatureDoesNotMatch</td>
      <td>제공한 서명이 규칙에 부합하지 않을 경우, 해당 오류 코드를 반환합니다.</td>
			<td nowrap="nowrap">403 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.3">Forbidden</a></td>
   </tr>
   <tr>
      <td>NoSuchBucket</td>
      <td>추가 시도한 규칙이 위치한 Bucket이 존재하지 않으면 해당 오류 코드를 반환합니다.</td>
			<td nowrap="nowrap">404 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td>
   </tr>
   <tr>
      <td>MalformedXML</td>
      <td>XML 형식이 잘못되었습니다. Restful API 문서와 자세히 비교하십시오.</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
   <tr>
      <td>InvalidRequest</td>
      <td>요청이 잘못되었습니다. 오류 설명에 "header acl and body acl conflict"가 표시되면 헤더와 body에 모두 acl 매개 변수가 있을 수 없다는 것을 의미합니다.</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
</table>

## 실제 사례

### 요청

```shell
PUT /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

<AccessControlPolicy>
   <Owner>
     <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
     <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
   </Owner>
   <AccessControlList>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
           <URI>http://cam.qcloud.com/groups/global/AllUsers</URI>
        </Grantee>
        <Permission>READ</Permission>
     </Grant>
     <Grant>
        <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
           <ID>qcs::cam::uin/1250000000:uin/1250000000</ID>
           <DisplayName>qcs::cam::uin/1250000000:uin/1250000000</DisplayName>
        </Grantee>
        <Permission>FULL_CONTROL</Permission>
     </Grant>
   </AccessControlList>
</AccessControlPolicy>
```

### 응답

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT\
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```

