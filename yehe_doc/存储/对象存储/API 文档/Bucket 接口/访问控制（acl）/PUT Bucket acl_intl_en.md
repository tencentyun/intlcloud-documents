## Overview

This API is used to write an access control list (ACL) for a bucket. You can set the ACL information through the `x-cos-acl` and `x-cos-grant-*` request headers or the request body in XML format.
>!
>- You can set the ACL information either through request headers or through the request body.
> - `PUT Bucket acl` is an overwriting operation. The new ACL will overwrite the old one.
>- With this API, you can grant permissions to Tencent Cloud CAM root accounts, anonymous users, and sub-users. To grant permissions to user groups, see [Associating/Unassociating Policy with/from User Group](https://intl.cloud.tencent.com/document/product/598/32666). For more information about ACL, see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).
> - To call this API, you need to have permission to write ACL to the bucket.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketAcl&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>




## Request

#### Sample request

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
>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header | Description | Type | Required |
| :----------------------- | :----------------------------------------------------------- | :----- | :------- |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` (default) and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E9.A2.84.E8.AE.BE.E7.9A.84-acl). | Enum | No |
| x-cos-grant-read         | Grants a user read access to a bucket in the format of `id="[OwnerUin]"` for root accounts such as `id="100000000001"` or `id="[OwnerUin/GrantsUin]"` for sub-accounts such as `id="100000000001/100000000011"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-write         | Grants a user write access to a bucket in the format of `id="[OwnerUin]"` for root accounts such as `id="100000000001"` or `id="[OwnerUin/GrantsUin]"` for sub-accounts such as `id="100000000001/100000000011"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-read-acp         | Grants a user read access to a bucket ACL in the format of `id="[OwnerUin]"` for root accounts such as `id="100000000001"` or `id="[OwnerUin/GrantsUin]"` for sub-accounts such as `id="100000000001/100000000011"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-write-acp        | Grants a user write access to a bucket ACL in the format of `id="[OwnerUin]"` for root accounts such as `id="100000000001"` or `id="[OwnerUin/GrantsUin]"` for sub-accounts such as `id="100000000001/100000000011"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |
| x-cos-grant-full-control         | Grants a user full access to a bucket in the format of `id="[OwnerUin]"` for root accounts such as `id="100000000001"` or `id="[OwnerUin/GrantsUin]"` for sub-accounts such as `id="100000000001/100000000011"`. You can separate multiple users by comma, such as `id="100000000001",id="100000000002"`. | string | No       |


#### Request body

The request body contains the **application/xml** data that includes information about the bucket owner and authorization.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| AccessControlPolicy | None | All request information about the `PUT Bucket acl` operation |Container| Yes |

**Content of `AccessControlPolicy`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| Owner | AccessControlPolicy | Information about the bucket owner |Container| Yes |
| AccessControlList | AccessControlPolicy | Information about the grantee and permissions | Container | Yes |

**Content of `Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| ID | AccessControlPolicy.Owner | Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]` <br> Example: `qcs::cam::uin/100000000001:uin/100000000001` | string | Yes |

**Content of `AccessControlList`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| Grant | AccessControlPolicy.AccessControlList | A single permission. Each `AccessControlList` supports up to 100 `Grant` nodes. | Container | Yes |

**Content of `AccessControlList.Grant`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| Grantee | AccessControlPolicy.AccessControlList.Grant | Grantee information. `xsi:type` can be set to `Group` or `CanonicalUser`. If it’s set to `Group`, the child node can only include `URI`. If it’s set to `CanonicalUser`, the child node can only include `ID`. | Container | Yes |
| Permission | AccessControlPolicy.AccessControlList.Grant | Permission granted. For the enumerated values such as `WRITE` and `FULL_CONTROL`, please see <b>Actions on buckets</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E6.93.8D.E4.BD.9C-permission) | Enum | Yes |

**Content of `AccessControlList.Grant.Grantee`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
---|---|---|---|---
| URI | AccessControlPolicy.AccessControlList.Grant.Grantee | Preset user group. For more information, please see <b>Preset user group</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E8.BA.AB.E4.BB.BD-grantee).<br>Example: `http://cam.qcloud.com/groups/global/AllUsers` or `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | string | Required if `xsi:type` of the `Grantee` is set to `Group` |
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | Compete ID of the grantee in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string | Required if `xsi:type` of the grantee is set to `CanonicalUser` |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Examples

#### Sample 1: configuring ACL through request headers

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

#### Sample 2: configuring ACL through the request body

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
