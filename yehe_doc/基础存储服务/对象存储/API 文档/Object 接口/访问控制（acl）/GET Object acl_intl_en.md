## Overview

This API is used to query the ACL of an object. To call this API, you need to have permission to read the ACL of the object.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetObjectAcl&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
GET /<ObjectKey>?acl HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns the **application/xml** data, which contains the object owner and authorization information.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| AccessControlPolicy | None | Stores the result of `GET Object acl`. | Container |

**Content of `AccessControlPolicy`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Owner | AccessControlPolicy | Information about the object owner | Container |
| AccessControlList | AccessControlPolicy | Information about the grantee and permissions |  Container |

**Content of `AccessControlPolicy.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | AccessControlPolicy.Owner | Complete ID of the object owner, formatted as `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string |
| DisplayName | AccessControlPolicy.Owner | Name of the object owner | string |

**Content of `AccessControlPolicy.AccessControlList`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Grant | AccessControlPolicy.AccessControlList | A single permission | Container |

**Content of `AccessControlPolicy.AccessControlList.Grant`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Grantee | AccessControlPolicy.AccessControlList.Grant | Grantee information. `xsi:type` can be set to `Group` or `CanonicalUser`. If `xsi:type` is set to `Group`, the child node can contain only `URI`. If `xsi:type` is set to `CanonicalUser`, the child node can contain only `ID` and `DisplayName`. | Container |
| Permission | AccessControlPolicy.AccessControlList.Grant | Permission granted. For the enumerated values, such as `READ` and `FULL_CONTROL`, please see <b>Actions on objects</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). | Enum |

**Content of `AccessControlPolicy.AccessControlList.Grant.Grantee`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| URI | AccessControlPolicy.AccessControlList.Grant.Grantee | Preset user group. For more information, please see <b>Preset user group</b> in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).<br>Example: `http://cam.qcloud.com/groups/global/AllUsers`, `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | string |
| ID | AccessControlPolicy.AccessControlList.Grant.Grantee | Compete ID of the grantee, formatted as `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string |
| DisplayName | AccessControlPolicy.AccessControlList.Grant.Grantee | Name of the grantee | string |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```shell
GET /exampleobject?acl HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 10 Sep 2019 08:29:26 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1568104166;1568111366&q-key-time=1568104166;1568111366&q-header-list=date;host&q-url-param-list=acl&q-signature=207b3066eaf73a81d80cf12bf9db594a1172****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 742
Connection: close
Date: Tue, 10 Sep 2019 08:29:26 GMT
Server: tencent-cos
x-cos-request-id: NWQ3NzVlZTZfYmIwMmEwOV83YTQ5XzEzNTcx****

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
			<Permission>READ_ACP</Permission>
		</Grant>
	</AccessControlList>
</AccessControlPolicy>
```
