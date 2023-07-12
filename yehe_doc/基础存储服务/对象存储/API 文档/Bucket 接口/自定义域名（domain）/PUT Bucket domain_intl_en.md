## Overview

This API is used to configure a custom domain for a bucket.

> !
> - You can add up to 20 custom domains. To add more, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
> - The custom domain supports 3 types of origin servers (default, static website, and global acceleration). To use a static website origin server, [enable a static website](https://intl.cloud.tencent.com/document/product/436/14984). To use a global acceleration origin server, [enable global acceleration](https://intl.cloud.tencent.com/document/product/436/33406).
> - By default, the root account has permission to add a custom domain to a bucket and can go to the [CAM console](https://console.cloud.tencent.com/cam/overview) to grant such permission to a sub-account by allowing it to call the `PutBucketDomain` API.

## Request

#### Sample request

```plaintext
PUT /?domain HTTP/1.1
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

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request body submits the **application/xml** data that includes all information about the custom domain of the bucket.

```xml
<DomainConfiguration>
	<DomainRule>
		<Status>Enum</Status>
		<Name>string</Name>
		<Type>Enum</Type>
	</DomainRule>
	<DomainRule>
		<Status>Enum</Status>
		<Name>string</Name>
		<Type>Enum</Type>
	</DomainRule>
</DomainConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------- | ------ | ----------------------------------------- | --------- | -------- |
| DomainConfiguration | None | All configurations of the `PUT Bucket domain` request | Container | No |

**Content of `DomainConfiguration`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------- | -------- | --------- | -------- |
| DomainRule         | DomainConfiguration | Domain entry | Container | Yes       |

**Content of `DomainRule`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Status             | DomainConfiguration.DomainRule | Domain status. Enumerated values:<br><li>`ENABLED`, <li>`DISABLED`    | Enum   | Yes       |
| Name               | DomainConfiguration.DomainRule | Full domain name                                                     | string | Yes       |
| Type | DomainConfiguration.DomainRule | Type of the origin server. Enumerated values: <br><li>`REST`: default origin server<li>`WEBSITE`: static website origin server<li>`ACCELERATE`: global acceleration origin server | Enum | Yes |
| ForcedReplacement  | DomainConfiguration.DomainRule | If the specified domain has been used for another bucket, you can use this node to forcibly use this domain for the current bucket. Currently, only CNAME is supported. Therefore, you need to point this domain’s CNAME to this bucket’s origin server domain (which can be the default origin server, static website origin server, or global acceleration origin server depending on `Type`) before calling this API. | Enum | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

#### Request

```plaintext
PUT /?domain HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Apr 2020 09:16:14 GMT
Content-Type: application/xml
Content-Length: 288
Content-MD5: WHjVNjOz7lW82VThLKf4Lg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1588151774;1588158974&q-key-time=1588151774;1588158974&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=domain&q-signature=5cd58e4c68125ee6c78d626089d12c41376a****
Connection: close

<DomainConfiguration>
	<DomainRule>
		<Status>ENABLED</Status>
		<Name>cos.cloud.tencent.com</Name>
		<Type>REST</Type>
	</DomainRule>
	<DomainRule>
		<Status>ENABLED</Status>
		<Name>www.cos.cloud.tencent.com</Name>
		<Type>WEBSITE</Type>
	</DomainRule>
</DomainConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 29 Apr 2020 09:16:15 GMT
Server: tencent-cos
x-cos-request-id: NWVhOTQ1ZGVfZTViOTJhMDlfMzA0MjJfMTEwMmJi****
```
