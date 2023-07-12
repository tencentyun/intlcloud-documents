## Overview

This API is used to write an access control list (ACL) to an object. You can set the ACL information through the `x-cos-acl` and `x-cos-grant-*` request headers or the request body in XML format.
> !
> - You can set the ACL information either through request headers or through the request body.
> - `PUT Object acl` is an overwriting operation. The new ACL will overwrite the old one.
> - You can only grant permissions to Tencent Cloud CAM root accounts or anonymous users. To grant permissions to sub-accounts or user groups, please use the [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) API. For more information about ACL, please see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).
> - To call this API, you need to have permission to write ACL to the object.
> 

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutObjectAcl&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>

## Requests

#### Sample requests

**Sample 1**

```shell
PUT /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: 0
Authorization: Auth String
```

**Sample 2**

```plaintext
PUT /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String



[Request Body]
```


>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-acl | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the <b>Preset ACL</b> section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E9.A2.84.E8.AE.BE.E7.9A.84-acl). Default value: `default` <br>**Note**: If you do not need access control for the object, set this header to `default` or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | Enum | No |
| x-cos-grant-read | Grants a user read permission for an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-read-acp | Grants a user read permission for the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-write-acp | Grants a user write permission for the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use commas (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |

#### Request body

The request body contains the **application/xml** request data, including information about the object owner and authorization.

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
| --- | --- | --- | --- | --- |
| AccessControlPolicy | None | All request information about the `PUT Object acl` operation | Container | Yes |

**Content of `AccessControlPolicy`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Owner | AccessControlPolicy | Information about the object owner | Container | Yes |
| AccessControlList | AccessControlPolicy | Information about the grantee and permissions | Container | Yes |

**Content of `AccessControlPolicy.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| ID | AccessControlPolicy.Owner | Complete ID of the object owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string | Yes |

**Content of `AccessControlPolicy.AccessControlList`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Grant | AccessControlPolicy.<br>AccessControlList | A single permission. Each `AccessControlList` supports up to 100 `Grant` nodes. | Container | Yes |

**Content of `AccessControlPolicy.AccessControlList.Grant`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Grantee | AccessControlPolicy.<br>AccessControlList.Grant | Grantee information. `xsi:type` can be set to `Group` or `CanonicalUser`. If set to `Group`, the child node can only include `URI`. If set to `CanonicalUser`, the child node can only include `ID`. | Container | Yes |
| Permission | AccessControlPolicy.<br>AccessControlList.Grant | Permission granted. For the enumerated values, such as `READ` and `FULL_CONTROL`, please see <b>Actions on objects</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E6.93.8D.E4.BD.9C-permission). | Enum | Yes |

**Content of `AccessControlPolicy.AccessControlList.Grant.Grantee`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| URI | AccessControlPolicy.<br>AccessControlList.Grant.Grantee | Preset user group. For more information, please see <b>Preset user group</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583#.E8.BA.AB.E4.BB.BD-grantee).<br>Example: `http://cam.qcloud.com/groups/global/AllUsers` or `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | string | Required if `xsi:type` of the grantee is set to `Group` |
| ID | AccessControlPolicy.<br>AccessControlList.Grant.Grantee | Compete ID of the grantee in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string | Required if `xsi:type` of the grantee is set to `CanonicalUser` |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: configuring ACL through request headers

#### Request

```shell
PUT /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 09 Sep 2019 13:11:09 GMT
x-cos-acl: public-read
x-cos-grant-read-acp: id="100000000002"
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1568034669;1568041869&q-key-time=1568034669;1568041869&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp&q-url-param-list=acl&q-signature=43faf0a3231435a922e16526709c281a537d****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Mon, 09 Sep 2019 13:11:10 GMT
Server: tencent-cos
x-cos-request-id: NWQ3NjRmNmRfZjZjMjBiMDlfMmE5MWJfMTI3OWZh****
```

#### Sample 2: configuring ACL through the request body

#### Request

``` shell
PUT /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 10 Sep 2019 06:32:02 GMT
Content-Type: application/xml
Content-Length: 594
Content-MD5: zUPEBc1TeGrqTqEfPV7rxg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1568097122;1568104322&q-key-time=1568097122;1568104322&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=acl&q-signature=edab1b68ce0f747604906354afbe5702b24c****
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
Date: Tue, 10 Sep 2019 06:32:02 GMT
Server: tencent-cos
x-cos-request-id: NWQ3NzQzNjJfZmVhODBiMDlfMjc5MGVfMTM4OTky****
```
