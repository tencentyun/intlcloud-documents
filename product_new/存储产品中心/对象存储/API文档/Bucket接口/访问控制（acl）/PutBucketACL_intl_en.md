## Description

This API is used to write an access control list (ACL) to a bucket. You can pass in the ACL information through the request headers `x-cos-acl` and `x-cos-grant-*` or through the request body in XML format.
>!
>- You can set the ACL information either through request headers or through the request body.
>- `PUT Bucket acl` is an overwriting operation. The new ACL passed in will overwrite the old one.
>- To make this request, you need to have the permission to write ACL to the bucket.

## Request

#### Sample Request

**Sample 1**
```shell
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: 0
Authorization: Auth String
```
**Sample 2**
```shell
PUT /?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

This API does not use any request parameter.

#### Request Headers

In addition to common request headers, this API also supports the following request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

Name | Description | Type | Required
---|---|---|---
x-cos-acl| Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
x-cos-grant-read| Allows grantee to read the bucket; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"`|string| No
x-cos-grant-write| Allows grantee to write to the bucket; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"`|string| No
x-cos-grant-read-acp| Allows grantee to read the ACL and the policy of the bucket; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"`|string| No
x-cos-grant-write-acp| Allows grantee to write to the ACL and the policy of the bucket; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"`|string| No
x-cos-grant-full-control| Grants a user full permission to perform operations on the bucket; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"`|string| No

#### Request Body

This request body submits the **application/xml** request data which include the bucket owner information and full authorization information.

```shell
<AccessControlPolicy>
	<Owner>
		<ID>string</ID>
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
			</Grantee>
			<Permission>Enum</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

The nodes are described in details below:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
AccessControlPolicy| None | All request information of the `PUT Bucket acl` operation |Container| Yes

**Content of the Container node `AccessControlPolicy`:**

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
Owner|AccessControlPolicy| Bucket owner information |Container| Yes
AccessControlList|AccessControlPolicy| Information on the grantee and permissions |Container| Yes

**Content of the Container node `Owner`:**

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
ID|AccessControlPolicy.Owner| Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`|string| Yes

**Content of the Container node `AccessControlList`:**

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
Grant|AccessControlPolicy.AccessControlList| A single permission entry. One `AccessControlList` can have up to 100 `Grant` entries |Container| Yes

**Content of the Container node `AccessControlList.Grant`:**

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
Grantee|AccessControlPolicy.AccessControlList.Grant| Grantee information. `xsi:type` can be specified as `Group` or `CanonicalUser`. If it is specified as `Group`, the child node includes and can only include `URI`. If it is specified as `CanonicalUser`, the child node includes and can only include `ID` |Container| Yes
Permission|AccessControlPolicy.AccessControlList.Grant| Permissions. For the enumerated values such as `WRITE` and `FULL_CONTROL`, see the “Actions on buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) |Enum| Yes

**Content of the Container node `AccessControlList.Grant.Grantee`:**

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
URI|AccessControlPolicy.AccessControlList.Grant.Grantee| Preset user group such as `http://cam.qcloud.com/groups/global/AllUsers` or `http://cam.qcloud.com/groups/global/AuthenticatedUsers`. For more information, see the “Preset user group” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) |string| Yes if `xsi:type` of `Grantee` is specified as `Group`
ID|AccessControlPolicy.AccessControlList.Grant.Grantee| Complete ID of the grantee in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`|string| Yes if `xsi:type` of `Grantee` is specified as `CanonicalUser`

## Response

#### Response Headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body

The response body of this API is empty.

#### Error Codes

The implementation of this operation returns the following special error messages. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
InvalidDigest| The given Content-MD5 checksum is invalid |400 Bad Request
MalformedXML| The XML format of the request body does not conform to the XML syntax |400 Bad Request

## Examples

#### Example 1. Configuring ACL through request headers

#### Request

```shell
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:30:12 GMT
x-cos-acl: public-read
x-cos-grant-write: id="100000000002"
x-cos-grant-read-acp: id="100000000002"
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760212;1560767412&q-key-time=1560760212;1560767412&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp;x-cos-grant-write&q-url-param-list=acl&q-signature=5b10c6ea4e6c9630c085e1f85476c76d8c4e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Mon, 17 Jun 2019 08:30:13 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzRmOTRfODhjMjJhMDlfMWRlYl81Mzc0****
```

#### Example 2. Configuring ACL through request body

#### Request

```shell
PUT /?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 17 Jun 2019 08:30:13 GMT
Content-Type: application/xml
Content-Length: 812
Content-MD5: 1qS+8SqnivarcO6Z11R0nw==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560760213;1560767413&q-key-time=1560760213;1560767413&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=acl&q-signature=70f96b91823f3715905df125d96fe447554e****
Connection: close

<AccessControlPolicy>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
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
			</Grantee>
			<Permission>WRITE</Permission>
		</Grant>
		<Grant>
			<Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
				<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
			</Grantee>
			<Permission>READ_ACP</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Mon, 17 Jun 2019 08:30:13 GMT
Server: tencent-cos
x-cos-request-id: NWQwNzRmOTVfMzBjMDJhMDlfOTM3MF8yNzdj****
```
