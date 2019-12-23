## 기능 설명
GET Object acl API는 어느 한 버킷의 객체 접근 권한을 획득하는 데 사용되며, 버킷 소유자만이 작업할 권한이 있습니다.

## 버전
기본 상황에서 해당 GET 작업은 객체의 현재 버전을 반환합니다. 다른 버전을 반환해야 할 경우, version Id 서브 리소스를 사용하십시오.

## 요청

요청 예시:
```
GET /ObjectName?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청행
~~~
GET /ObjectName?acl HTTP/1.1
~~~
해당 API는 GET 요청을 수신합니다.

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더
**필수 헤더**
해당 요청 작업은 다음 필수 헤더를 사용하여 구현됩니다.

|이름|설명|유형|필수 선택 여부|
|:---|:-- |:--|:--|
| Authorization | 서명 문자열 |String| 예 |

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.
### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.

```
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
    <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
      <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
      <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
      </Grantee>
      <Permission></Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/<OwnerUin>:uin/<SubUin></ID>
        <DisplayName>qcs::cam::uin/<OwnerUin>:uin/<SubUin></DisplayName>
      </Grantee>
      <Permission></Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

구체적인 데이터 내용은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| AccessControlPolicy |없음| GET Object acl 결과를 저장하는 컨테이너 | Container |

Container 노드 AccessControlPolicy의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| Owner | AccessControlPolicy | 객체 소유자 정보 |  Container |
| AccessControlList | AccessControlPolicy | 권한을 부여받은 자의 정보와 권한 정보 |  Container |

Container 노드 Owner의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| ID | AccessControlPolicy.Owner |  객체 소유자 ID, </br>형식: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt; 루트 계정일 경우, &lt;OwnerUin&gt; 와 &lt;SubUin&gt;는 동일한 값입니다. |  String |
| DisplayName | AccessControlPolicy.Owner |  객체 소유자의 이름 |  String |

Container 노드 AccessControlList의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| Grant | AccessControlPolicy.AccessControlList | 단일 객체의 권한 정보입니다. 1개의 AccessControlList는 100개의 Grant를 보유할 수 있습니다. | Container    |

Container 노드 Grant의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 정보를 설명합니다. type 유형은 RootAccount, Subaccount가 가능합니다. type 유형이 RootAccount일 경우, ID에서 지정한 것은 루트 계정이며, type 유형이 Subaccount일 경우, ID에서 지정한것은 서브 계정입니다.| Container    |
| Permission | AccessControlPolicy.AccessControlList.Grant | 권한을 부여받은 자의 권한 정보를 지정합니다. 열거형 값: READ, WRITE, FULL_CONTROL  | String    |

Container 노드 Grantee의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | AccessControlPolicy.Owner | 사용자의 ID, 루트 계정일 경우, 형식은 qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt; 또는 qcs::cam::anyone:anyone(모든 사용자를 대신함)이며, 서브 계정일 경우, 형식은 qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;입니다.|  String |
| DisplayName | AccessControlPolicy.Owner |  사용자의 이름 |  String |


## 실제 사례

### 요청1
```
GET /ObjectName?acl HTTP/1.1
Host: zuhaotestnorth-1251668577.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b40652
```

### 응답1
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 266
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==

<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/12345:uin/12345</ID>
    <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/12345:uin/12345</ID>
        <DisplayName>qcs::cam::uin/12345:uin/12345</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RootAccount">
        <ID>qcs::cam::uin/54321:uin/54321</ID>
        <DisplayName>qcs::cam::anyone:anyone</DisplayName>
      </Grantee>
      <Permission>READ</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```
