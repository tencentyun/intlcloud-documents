## Description

This API is used to get the access control list (ACL) of a bucket. To make this request, you need to have the permission to read the ACL of the bucket.

## Request

#### Sample Request

```shell
GET /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body

A successful query will return **application/xml** data which include the bucket owner information and full authorization information.

```shell
<AccessControlPolicy>
	<Owner>
		<ID>string</ID>
		<DisplayName>string</DisplayName>
	</Owner>
	<AccessControlList>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Group">
				<URI>string</URI>
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>string</ID>
				<DisplayName>string</DisplayName>
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

The nodes are described in details below:

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
AccessControlPolicy| None | Stores the result of the `GET Bucket acl` operation |Container

**Content of the Container node `AccessControlPolicy`:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Owner|AccessControlPolicy| Bucket owner information |Container
AccessControlList|AccessControlPolicy| Information on the grantee and permissions |Container

**Content of the Container node `Owner`:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
ID|AccessControlPolicy.Owner| Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`|string
DisplayName|AccessControlPolicy.Owner| Bucket owner name |string

**Content of the Container node `AccessControlList`:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Grant|AccessControlPolicy.AccessControlList| A single permission entry |Container

**Content of the Container node `AccessControlList.Grant`:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
Grantee|AccessControlPolicy.AccessControlList.Grant| Grantee information. If `xsi:type` is specified as `Group`, the child node includes and only includes `URI`. If it is specified as `CanonicalUser`, the child nodes include and only include `ID` and `DisplayName` |Container
Permission|AccessControlPolicy.AccessControlList.Grant| Permissions. For the enumerated values such as `WRITE` and `FULL_CONTROL`, see the “Actions on buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) |Enum

**Content of the Container node `AccessControlList.Grant.Grantee`:**

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
URI|AccessControlPolicy.AccessControlList.Grant.Grantee| Preset user group such as `http://cam.qcloud.com/groups/global/AllUsers` or `http://cam.qcloud.com/groups/global/AuthenticatedUsers`. For more information, see the “Preset user group” section in [ACL Overview](https://cloud.tencent.com/document/product/436/30752#.E8.BA.AB.E4.BB.BD-grantee) |string
ID|AccessControlPolicy.AccessControlList.Grant.Grantee| Complete ID of the grantee in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`|string
DisplayName|AccessControlPolicy.AccessControlList.Grant.Grantee| Grantee name |string

#### Error Codes

There is no special error message for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

#### Request

```shell
GET /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:37:35 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760655;1560767855&q-key-time=1560760655;1560767855&q-header-list=date;host&q-url-param-list=acl&q-signature=24b9d377eac860917a33c8c298042ce5b1a5****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1035
Connection: close
Date: Mon, 17 Jun 2019 08:37:36 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzUxNTBfMzdiMDJhMDlfOWM0Nl85NDFk****

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
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
				<DisplayName>qcs::cam::uin/100000000002:uin/100000000002</DisplayName>
			</Grantee>
			<Permission>WRITE</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
				<DisplayName>qcs::cam::uin/100000000002:uin/100000000002</DisplayName>
			</Grantee>
			<Permission>READ_ACP</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```
