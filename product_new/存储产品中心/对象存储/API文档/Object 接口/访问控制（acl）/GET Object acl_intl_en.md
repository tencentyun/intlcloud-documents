## Description
This API (GET Object acl) is used to get the access permission to the specified object in the specified bucket. Only the bucket owner has permission to manipulate it.

### Version
By default, the GET operation will return the current version of the object. If you want to return a different version, use the versionId sub-resource.

## Request
### Sample Request
```shell
GET /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
**Required headers**
The implementation of this request operation uses the following required request headers:

| Name | Description | Type | Required |
|:---|:-- |:--|:--|
| Authorization | Signature string | String | Yes |

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.
### Response Body
The return of this response body is **application/xml** data. Below is a sample containing all the node data:

```shell
<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
    <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
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
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
        <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
     </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| AccessControlPolicy | None | Container for storing the GET Object acl result | Container |

Content of the Container node AccessControlPolicy:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Owner | AccessControlPolicy | Object owner information | Container |
| AccessControlList | AccessControlPolicy | Information of grantee and permission |  Container |

Content of the Container node Owner:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| ID | AccessControlPolicy.Owner |  Object owner ID. </br>Format: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;. If it is a root account, &lt;OwnerUin&gt; and &lt;SubUin&gt; are the same value |  String |
| DisplayName | AccessControlPolicy.Owner |  Object owner name |  String |

Content of the Container node AccessControlList:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| Grant | AccessControlPolicy.AccessControlList | Authorization information of a single object. An AccessControlList can have 100 Grant entries | Container |

Content of the Container node Grant:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| Grantee | AccessControlPolicy.AccessControlList.Grant | Describes the information of the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | Container |
| Permission | AccessControlPolicy.AccessControlList.Grant | Specifies the permission granted to the grantee. Enumerated values: READ, FULL_CONTROL  | String    |

Content of the Container node Grantee:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
|URI|  AccessControlPolicy.AccessControlList.Grant.Grantee| Specifies all users |  String |
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | User ID in the format of qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;. If it is a root account, &lt;OwnerUin&gt; and &lt;SubUin&gt; are the same value |  String |
| DisplayName | AccessControlPolicy.AccessControlList.Grant.Grantee |  Username |  String |


## Samples

### Request
```shell
GET /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4065
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 266
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==

<AccessControlPolicy>
  <Owner>
    <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
    <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
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
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
        <DisplayName>qcs::cam::uin/100000000001:uin/100000000001</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
     </Grant>
  </AccessControlList>
</AccessControlPolicy>
```
