## Description
This API (PUT Object acl) is used to configure an ACL table for the specified object in the specified bucket. You can pass in the ACL information through the "x-cos-acl", "x-cos-grant-read", and "x-cos-grant-full-control" headers or through the request body in XML format.

## Request
#### Sample Request

```shell
PUT /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Header

#### Common Headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

<table>
   <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-acl</td>
      <td>It defines the ACL attribute of the object. Value range: private, public-read, default. Default value: default (i.e., inheriting the bucket's permission); <br>Note: Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permission of the bucket</td>
      <td>string</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-read</td>
      <td>Grants the grantee read permission in the format of x-cos-grant-read: id="[OwnerUin]"</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td nowrap="nowrap">x-cos-grant-full-control</td>
      <td>Grants the grantee full permission in the format of x-cos-grant-full-control: id="[OwnerUin]"</td>
      <td>String</td>
      <td>No</td>
   </tr>
</table>


#### Request Body
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

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:---|
| AccessControlPolicy | None | Container for storing the GET Object acl result | Container | Yes |

Content of the Container node AccessControlPolicy:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:---|
| Owner | AccessControlPolicy | Object owner information | Container | Yes |
| AccessControlList | AccessControlPolicy | Information of grantee and permission |  Container | Yes |

Content of the Container node Owner:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:---|
| ID | AccessControlPolicy.Owner |  Object owner ID. </br>Format: qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;. <br>If it is a root account, &lt;OwnerUin&gt; and &lt;SubUin&gt; are the same value |  String | Yes |
| DisplayName | AccessControlPolicy.Owner |  Object owner name |  String | Yes |

Content of the Container node AccessControlList:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------ | ------------------------------------- | --------- |:--|:---|
| Grant | AccessControlPolicy.AccessControlList | Authorization information of a single object. An AccessControlList can have 100 Grant entries | Container | Yes |

Content of the Container node Grant:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------ | ------------------------------------- | --------- |:--|:---|
| Grantee | AccessControlPolicy.AccessControlList.Grant | Describes the information of the grantee. The type can be RootAccount or Subaccount. <br><li>If the type is RootAccount, the ID specifies a root account. <br><li>If the type is Subaccount, the ID specifies a sub-account | Container | Yes |
| Permission | AccessControlPolicy.AccessControlList.Grant | Specifies the permission granted to the grantee. Enumerated values: READ, FULL_CONTROL  | String    | Yes |

Content of the Container node Grantee:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------ | ------------------------------------- | --------- |:--|:---|
|URI|  AccessControlPolicy.AccessControlList.Grant.Grantee| Specifies all users |  String | Yes |
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | User ID in the format of qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;. <br>If it is a root account, &lt;OwnerUin&gt; and &lt;SubUin&gt; are the same value |  String | Yes |
| DisplayName | AccessControlPolicy.AccessControlList.Grant.Grantee |  Username |  String | Yes |


## Response
#### Response Header

#### Common Response Headers

This response uses a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This request operation has no special response headers.

#### Response Body
The response body of this request is empty.

#### Error Codes
The following error messages may be present in this response. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

<table>
   <tr>
      <th>Error Code</th>
      <th>Description</th>
      <th>HTTP Status Code</th>
   </tr>
   <tr>
      <td>SignatureDoesNotMatch</td>
      <td>If the provided signature does not conform to the rule, this error code will be returned</td>
			<td nowrap="nowrap">403 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.3">Forbidden</a></td>
   </tr>
   <tr>
      <td>NoSuchBucket</td>
      <td>If the bucket to which you want to add the rule does not exist, this error code will be returned</td>
			<td nowrap="nowrap">404 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td>
   </tr>
   <tr>
      <td>MalformedXML</td>
      <td>Invalid XML format. Please check against the Restful API documentation</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
   <tr>
      <td>InvalidRequest</td>
      <td>The request is invalid. If the error message shows "header acl and body acl conflict", it means that the header and body cannot set the acl parameter at the same time</td>
			<td nowrap="nowrap">400 <a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td>
   </tr>
</table>

## Examples

#### Request

```shell
PUT /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484724784;32557620784&q-key-time=1484724784;32557620784&q-header-list=host&q-url-param-list=acl&q-signature=785d9075b8154119e6a075713c1b9e56ff0bddfc
Content-Length: 229
Content-Type: application/x-www-form-urlencoded

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

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT\
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```
